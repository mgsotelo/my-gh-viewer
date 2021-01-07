<template>
  <div>
    <h2>Commits</h2>
    <div class="scrollme">
      <single-commit-view
        @commitClicked="emitCommit($event)"
        v-for="commit in thecommits"
        :key="commit.sha"
        :title="commit.commit.message | onlyTitle"
        :description="commit.commit.message | onlyDesc"
        :userCommit="commit.commit.author.name"
        :ago="commit.commit.committer.date | ago"
        :refer="commit.sha"
      >
      </single-commit-view>
    </div>
  </div>
</template>

<script>
import SingleCommitView from './SingleCommitView';
const axios = require('axios').default;
const moment = require('moment');

export default {
  data() {
    return {
      thecommits: [],
    };
  },

  filters: {
    onlyTitle: function (text) {
      if (!text) return '';
      var regexstring = new RegExp('.+[^\\n]', 'g');
      return regexstring.exec(text)[0];
    },

    onlyDesc: function (text) {
      if (!text) return '';
      var regexstring = new RegExp('[\\n]{2}(.+)', 'g');
      var result = regexstring.exec(text);
      if (result === null) {
        return 'No description';
      } else {
        return result[1];
      }
    },

    ago: function (date) {
      moment().format();
      return moment(date).fromNow();
      // return date;
    },
  },

  props: {
    repo: {
      type: String,
      default: 'mgsotelo/my-gh-viewer',
    },
  },
  components: {
    SingleCommitView,
  },

  methods: {
    async commits() {
      try {
        const response = await axios.get('https://api.github.com/repos/' + this.repo + '/commits');
        console.log(response.data);
        return response.data;
      } catch (error) {
        console.log(error);
      }
    },

    async emitCommit(sha) {
      // console.log(sha)
      const response = await axios.get('https://api.github.com/repos/' + this.repo + '/commits/' + sha)
      console.log(response.data)
      this.$emit('commitRequired', response.data)
    }
  },

  async mounted() {
    this.thecommits = await this.commits();
  },
};
</script>

<style scoped>
.scrollme {
  max-height: 600px;
  overflow: scroll;
}

h2 {
  text-align: left;
}
</style>
