<template>
<div class="card container mb-4">
  <h3 class="pt-2">{{ title }}</h3>
  <button @click="openNews" class="btn btn-success mb-2" >{{ isNewOpen ? "Закрыть новость" : "Открыть новость" }}</button>
  <p v-if="isNewOpen">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Facere fugit ipsum iure libero magnam modi molestiae nam quae quibusdam sapiente. Ab aliquid consequuntur culpa deleniti dolores enim expedita iure laborum libero minus modi necessitatibus perspiciatis quaerat quibusdam saepe vitae, voluptatem!</p>
</div>
</template>

<script>
export default {
  name: "AppNews.vue",
  props: {
    title: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    },
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      validator(value) {
        return value == true || value == false
      }
    }
  },
  data() {
    return {
      isNewOpen: this.isOpen
    }
  },
  methods: {
    openNews() {
      this.isNewOpen = !this.isNewOpen
      if(this.isNewOpen) {
        this.$emit('open-news')
      }

    }
  }
}
</script>

<style scoped>
button {
  width: 220px;
  margin: 0 auto;
}
</style>
