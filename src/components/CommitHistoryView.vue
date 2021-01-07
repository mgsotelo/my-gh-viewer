<template>
  <div>
    <h2>Commits</h2>
    <div class="scrollme">
      <single-commit-view
        v-for="commit in thecommits"
        :key="commit.id"
        :title="commit.commit.message | onlyTitle"
        :description="commit.commit.message | onlyDesc"
        :userCommit="commit.commit.author.name"
        :ago="commit.commit.committer.date | ago"
      >
      </single-commit-view>
    </div>
  </div>
</template>

<script>
import SingleCommitView from './SingleCommitView';
const axios = require('axios').default;
const moment = require('moment'); // require

export default {
  data() {
    return {
      thecommits: [],
    };
  },

  filters: {
    onlyTitle: function (wtf) {
      if (!wtf) return '';
      var regexstring = new RegExp('.+[^\\n]', 'g');
      return regexstring.exec(wtf)[0];
    },

    onlyDesc: function (wtf) {
      if (!wtf) return '';
      var regexstring = new RegExp('[\\n]{2}(.+)', 'g');
      var omg = regexstring.exec(wtf);
      // console.log(omg)
      if (omg === null) {
        return 'No description';
      } else {
        return omg[1];
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
  },

  async mounted() {
    this.thecommits = await this.commits();
  },
};
</script>

<style scoped>
.scrollme {
  height: 80%;
  overflow: scroll;
}

</style>
