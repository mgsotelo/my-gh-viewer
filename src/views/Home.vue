<template>
  <b-container>
    <b-row class="myheader">
      <h1><a :href="'https://github.com/'+theRepo()"> {{theRepo()}} </a></h1>
    </b-row>

    <b-row>
      <b-col cols="3">asdasd</b-col>
      <b-col cols="9"> xdxdd </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  methods: {
    theRepo() {
      return 'mgsotelo/my-gh-viewer';
    },
  },
};
</script>

<style scoped>
.myheader {
  background-color: #d3d3f2;
  margin-bottom: 1%;
}
</style>
