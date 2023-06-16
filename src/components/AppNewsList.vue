<template>
  <hr/>
  <h4>{{ title }}</h4>
<ul>
  <li class="list-group-item" v-for="item in news">{{ item.title }}<span v-if="item.wasRead">!!!</span></li>
</ul>
</template>

<script>
export default {
  name: "AppNewsList.vue",
  inject: ['title', 'news']
}
</script>

<style scoped>

</style>
