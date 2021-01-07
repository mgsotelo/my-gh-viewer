<template>
  <div class="mybordered">
    <a href="#" rel="noopener noreferrer" @click="referMe"><span>{{refer}}</span></a>
    <h4>{{ title }}</h4>
    <p class="desc">
      {{ description }} - by <strong>{{ userCommit }}</strong>
    </p>
    <p class="time">{{ ago }}</p>
  </div>
</template>

<script>
export default {
  props: {

    refer:{
      type:String,
      default: ""
    },
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

  methods: {
    referMe() {
      this.$emit('commitClicked', this.$props.refer)
    }
  },


};
</script>

<style scoped>
span {
  font-size: 9px;
}
.mybordered {
  margin: 3px;
  padding: 10px;
  border: solid #1a1a1a1a 0.5px;
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

.mybordered p.time {
  color: #292626;
  font-size: 12px;
  text-align: right;
}
</style>
