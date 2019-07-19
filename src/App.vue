<template>
  <div id="app" class="container">
    <h1>Components Dinamicos</h1>
    <button @click="componentSelecionado = 'Home'">Home</button>
    <button @click="componentSelecionado = 'PostsLista'">Posts Lista</button>
    <button @click="componentSelecionado = 'Sobre'">Sobre</button>
    <button @click="componentSelecionado = 'Assincrono'">Assincrono</button>

    <keep-alive include="Sobre">
      <component
      :is="componentSelecionado"
      v-bind="propsAtuais"
      ></component>
    </keep-alive>

  </div>
</template>

<script>
import Home from './components/Home.vue'
import Sobre from './components/Sobre.vue'
import PostsLista from './components/PostsLista.vue'

export default {
  components: {
    Assincrono:  () => ({
      component: new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(import("./components/Assincrono.vue"))
          //reject('Carregamento falhou');
        }, 2000)
      }),
      loading: { template: '<p>Carregando</p>'},
      error: { template: '<p>Error ao carregar component</p>'},
      delay: 200,
      timeout: 3000,
    }),
    PostsLista,
    Home,
    Sobre
  },
  data () {
    return {
      componentSelecionado: 'Home',
      posts: [
        { id: 1, titulo: 'Componets Vue', conteudo: 'Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry', autor: 'Adailson' },
        { id: 2, titulo: 'Componets Vue 2', conteudo: 'Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry', autor: 'Adailson' }
      ]
    }
  },
  computed: {
    propsAtuais () {
      return this.componentSelecionado === 'PostsLista'
        ? { posts: this.posts }
        : {}
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
