<template>
  <div class="post" v-for="post in posts" :key="post.id">
    <div>
      <strong>{{ post.title }}:</strong> {{ post.body }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    posts: {
      type: String,
      required: true,
    },
  },
  data() {
    return {}
  },
  methods() {},
}
</script>

<style scoped>
.post {
  padding: 15px;
  border-radius: 10px;
  border: 2px solid teal;
  margin: 15px;
}
</style>
