<template>
  <h1>Актуальные новости {{ now }}</h1>
  <span>Открыто:{{ openRate }} </span>
<app-news
    v-for="item in news"
    :title="item.title"
    :key="item.id"
    :id="item.id"
    :is-open="item.isOpen"
    @open-news=openNews
></app-news>
</template>

<script>

import AppNews from "@/components/AppNews.vue";

export default {
  name: 'App',
  components: {AppNews},
  data () {
    return {
      now: new Date().toLocaleDateString(),
      openRate: 0,
      news: [
        {
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Labore, saepe',
          id: 1,
          isOpen: false
        },
        {
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam, doloremque temporibus?',
          id: 2,
          isOpen: false
        },
        {
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Corporis pariatur perferendis suscipit voluptate?',
          id: 3,
          isOpen: false
        }
      ]
    }
  },
  methods: {
    openNews() {
      this.openRate++
    }
  }

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
