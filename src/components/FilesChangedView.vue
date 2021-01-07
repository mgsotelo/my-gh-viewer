<template>
  <div>
    <h2>Files changed</h2>
    <span>{{ sha }}</span>
    <div class="scrollme">
      <div v-for="file in files" :key="file.id">
        {{ file }}
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

</style>
