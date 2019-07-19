<template>
  <div id="app" class="container">
    <h1>Vue JS</h1>
    <Post titulo="Components no Vue">
      <h2 slot="cabecalho">Components no Vue</h2>
      <p class="post-paragrafo">Lorem ipsum dolor, sit amet consectetur
      adipisicing elit. Quia, maiores ipsa pariatur dolorum, est 
      temporibus eaque illum corrupti, nostrum similique veritatis
      adipisci! Enim cum qui eum placeat dolor! Itaque, vero!</p>
      <span>...</span>
       <small slot="rodape">Por {{ autor }}</small>
    </Post>
  </div>
</template>

<script>
import Post from './components/Post.vue'
export default {
  components: {
    Post
  },
  data() {
    return {
      autor: 'Adailson'
    }
  }
}
</script>

<style scoped>
  .container {
    width: 960px;
    margin: auto;
  }
</style>
