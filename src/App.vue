<template>
  <h1>Актуальные новости {{ now }}</h1>
  <span>Открыто:{{ openRate }} | Прочитано:{{ readRate }}</span>
<app-news
    v-for="item in news"
    :title="item.title"
    :key="item.id"
    :id="item.id"
    :is-open="item.isOpen"
    :was-read="item.wasRead"
    @open-news=openNews
    @read-news=readNews
    @no-read-news=noReadNews
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
      readRate: 0,
      news: [
        {
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Labore, saepe',
          id: 1,
          isOpen: false,
          wasRead: false
        },
        {
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam, doloremque temporibus?',
          id: 2,
          isOpen: false,
          wasRead: false
        },
        {
          title: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Corporis pariatur perferendis suscipit voluptate?',
          id: 3,
          isOpen: false,
          wasRead: false
        }
      ]
    }
  },
  methods: {
    openNews() {
      this.openRate++
    },
    readNews(id) {
      let idx = this.news.findIndex(news => news.id === id)
      this.news[idx].wasRead = true
      this.readRate++
    },
    noReadNews(id) {
      let idx = this.news.findIndex(news => news.id === id)
      this.news[idx].wasRead = false
      this.readRate--
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
