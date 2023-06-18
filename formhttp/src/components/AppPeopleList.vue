<template>
  <div v-if="people.length !== 0">
  <div
      class="card mb-2 d-flex flex-row justify-content-between"
       v-for="person in people"
       :key="person.id">
    <h2 class="ps-3">{{ person.firstName }}</h2>
    <button
        @click="$emit('delete',person.id)"
        class="btn btn-outline-danger btn-sm">Удалить</button>
  </div>
  </div>
  <div v-else>
    <h4>Список пуст</h4>
    <button @click="$emit('load')"
            class="btn btn-outline-primary mt-3">Загрузить список</button>
  </div>
</template>

<script>
export default {
  emits:['load','delete'],
  name: "AppPeopleList.vue",
  props:['people']
}
</script>

<style scoped>

</style>
