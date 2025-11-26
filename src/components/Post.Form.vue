<template >
  <form @submit.prevent>
    <h4>Add the Post</h4>
    <input v-model="post.title" class="input" type="text" placeholder="title" />
    <input v-model="post.body" class="input" type="text" placeholder="description" />
    <button class="btn" @click="addPost">Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
    }
  },
  methods: {
    inputTitle(e) {
      this.post.title = e.target.value
    },

    addPost(e) {
      e.stopPropagation()
      e.preventDefault()

      this.post.id = new Date()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: '',
      }
    },
  },
}
</script>

<style scoped>
form {
  width: 100%;
  padding: 15px;
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  padding: 10px 15px;
  border: 1px solid teal;

  border-radius: 10px;
  margin-top: 10px;
}

.btn {
  margin-top: 15px;
  padding: 10px 45px;
  color: white;
  align-self: flex-end;
  background: teal;
  border: 1px solid teal;
  border-radius: 10px;
}
</style>


