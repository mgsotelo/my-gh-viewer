<template>
  <div>
    <h2>Files changed</h2>
    <span>{{ sha }}</span>
    <div class="scrollme">
      <div class="file" v-for="file in files" :key="file.id">
        <!-- {{ file }} -->
        <span>
          <a target="_blank" :href="file.blob_url">{{ file.filename }} </a>
        </span>
        <span> <div class="inline addition"></div> {{file.additions}} additions. </span>
        <span> <div class="inline deletion"></div> {{file.deletions}} deletions. </span>
        
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    files: {
      type: Array,
      default: () => [],
    },

    sha: {
      type: String,
      default: '',
    },
  },
};
</script>

<style scoped>
span {
  font-size: 12px;
}

.scrollme {
  max-height: 584px;
  overflow: scroll;
}

.file {
  display: block;
  border: solid #1c1c1c1c 0.5px;
  margin: 3px;
}

.inline {
  display: inline-block;
  border: solid #1c1c1c1c 0.5px;
  min-height: 10px;
  min-width: 10px;
}

.inline.addition {
  background-color: green;
}

.inline.deletion {
  background-color: red;
}
</style>
