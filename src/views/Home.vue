<template>
  <b-container>
    <b-row class="myheader">
      <h1>
        <a :href="'https://github.com/' + theRepo()"> {{ theRepo() }} </a>
      </h1>
    </b-row>

    <b-row>
      <b-col cols="4">
        <!-- aqui va el CommitHistoryView (union de varios SingleCommitViews) -->
        <commit-history-view @commitRequired="viewCommit($event)"></commit-history-view>
      </b-col>
      <b-col cols="8">
        <!-- aqui van los archivos cambiados de cada Commit (FilesChangedView) -->
        <files-changed-view :sha="commitDetailsSha" :files="commitFiles"></files-changed-view>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import CommitHistoryView from "../components/CommitHistoryView"
import FilesChangedView from "../components/FilesChangedView"
export default {

  data() {
    return {
      commitDetailsSha: "",
      commitFiles: []
    }
  },
  methods: {
    theRepo() {
      return 'mgsotelo/my-gh-viewer';
    },

    viewCommit(commit) {
      this.commitDetailsSha = commit.sha
      this.commitFiles = commit.files
    }
  },

  components: {
    CommitHistoryView,
    FilesChangedView
  },
};
</script>

<style scoped>
.myheader {
  background-color: #c0305b70;
  margin-bottom: 1%;
}
</style>
