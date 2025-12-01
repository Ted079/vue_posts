<template>
  <div class="post">
    <div>
      <strong>{{ post.title }}:</strong> {{ post.body }}
    </div>
    <div class="post__btns">
      <my-button @click="$emit('remove', post)">Delete</my-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: { type: Object, required: true },
  },
}
</script>


<style scoped>
.post {
  padding: 15px;
  border-radius: 10px;
  border: 2px solid teal;
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
  font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;
  font-size: 15px;
}
</style>