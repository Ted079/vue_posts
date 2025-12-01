<template>
  <div class="wrapper">
    <div v-if="posts.length > 0">
      <h3>Posts</h3>
      <TransitionGroup name="list" tag="ul">
        <post-item
          v-for="post in posts"
          :key="post.id"
          :post="post"
          @remove="$emit('remove', post)"
        />
      </TransitionGroup>
    </div>
    <div v-else>
      <h2 style="color: red">The post list is empty.</h2>
    </div>
  </div>
</template>

<script>
import PostItem from './PostItem.vue'
export default {
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: String,
      required: true,
    },
  },
  data() {
    return {}
  },
  methods: {},
}
</script>

<style>
h3 {
  margin-left: 15px;
  font-family: Arial, Helvetica, sans-serif;
  color: teal;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
