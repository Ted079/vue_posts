<template>
  <div class="app">
    <h1>My Posts</h1>

    <my-input style="margin-bottom: 5px" placeholder="Search.." v-model="searchQuery" />
    <div class="app__btns">
      <my-button style="margin: 15px 0" @click="changeVisibility">Add post</my-button>
      <my-select v-model="selectedSort" :options="selectedOption" />
    </div>
    <my-dialogue v-model:show="dialogueVisibility">
      <post-form @create="addPost" />
    </my-dialogue>
    <post-list v-if="!isLoadind" @remove="removePost" :posts="sortedAndFilteredPosts" />
    <div v-else>Loading...</div>
  </div>
</template>


<script>
import PostForm from './components/Post.Form.vue'
import PostList from './components/PostList.vue'
import MyButton from './components/UI/MyButton.vue'
import MyDialogue from './components/UI/MyDialogue.vue'
import MySelect from './components/UI/MySelect.vue'
import axios from 'axios'

export default {
  components: {
    PostForm,
    PostList,
    MyDialogue,
    MyButton,
    MySelect,
  },
  data() {
    return {
      posts: [],
      dialogueVisibility: false,
      isLoadind: true,

      searchQuery: '',
      selectedSort: '',
      selectedOption: [
        { value: 'title', name: 'sort by title' },
        { value: 'body', name: 'sort by description' },
      ],
    }
  },
  methods: {
    addPost(post) {
      this.posts.push(post)
      this.dialogueVisibility = false
    },

    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id)
    },

    changeVisibility() {
      this.dialogueVisibility = true
    },

    async fetchPosts() {
      try {
        this.isLoadind = true
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = response.data
      } catch (error) {
        console.log(error)
      } finally {
        this.isLoadind = false
      }
    },
  },

  mounted() {
    this.fetchPosts()
  },

  computed: {
    sortedPosts() {
      if (!this.selectedSort) return this.posts
      return [...this.posts].sort((post1, post2) =>
        post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
      )
    },

    sortedAndFilteredPosts() {
      return this.sortedPosts.filter((post) => post.title.includes(this.searchQuery))
    },
  },

  watch: {},
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

h1 {
  font-family: Arial, Helvetica, sans-serif;
  color: teal;
}
.app {
  margin: 40px;
}

.app__btns {
  display: flex;
  justify-content: space-between;
}
</style>