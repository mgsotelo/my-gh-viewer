<template>
  <div class="mybordered">
    <h4>{{ title }}</h4>
    <p class="desc">
      {{ description }} - by <strong>{{ userCommit }}</strong>
    </p>
    <p>{{ ago }}</p>
  </div>
</template>

<script>
export default {
  props: {
    repo: {
      type: String,
      default: 'mgsotelo/my-gh-viewer',
    },

    title: {
      type: String,
      default: '',
    },

    description: {
      type: String,
      default: '',
    },

    ago: {
      type: String,
      default: '',
    },

    userCommit: {
      type: String,
      default: '',
    },
  },
};
</script>

<style scoped>
.mybordered {
  border-color: #1c1c1c;
  border-width: 3px;
  background-color: rgba(25, 184, 25, 0.123);
  text-align: left;
}

.mybordered h4 {
  font-size: 16px;
  font-weight: 600;
}

.mybordered p.desc {
  font-size: 14px;
}
</style>
