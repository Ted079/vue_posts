<template>
  <div class="app">
    <post-form @create="addPost" />
    <post-list v-bind:posts="posts" />
    <!--:posts="posts"-->
  </div>
</template>


<script>
import PostForm from './components/Post.Form.vue'
import PostList from './components/PostList.vue'

export default {
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [
        { id: 1, title: 'JavaScript Basics', body: 'Что такое JS и зачем он нужен' },
        {
          id: 2,
          title: 'Vue 3 Composition API',
          body: 'Пишем компоненты на современном Vue',
        },
        { id: 3, title: 'Асинхронность в JS', body: 'Promise, async/await простым языком' },
        { id: 4, title: 'Работа с API', body: 'Как делать запросы и получать данные' },
      ],
    }
  },
  methods: {
    addPost(post) {
      this.posts.push(post)
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>