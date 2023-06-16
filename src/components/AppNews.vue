<template>
<div class="card container mb-4">
  <h3 class="pt-2">{{ title }}</h3>
  <app-button
      @action="openNews"
      color="btn-success">{{ isNewOpen ? "Закрыть новость" : "Открыть новость" }}
  </app-button>
  <app-button
      v-if="wasRead"
      color="btn-secondary"
      @action="noReadNews">Отметить непрочитанной
  </app-button>
  <div v-if="isNewOpen">
    <hr/>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Facere fugit ipsum iure libero magnam modi molestiae nam quae quibusdam sapiente. Ab aliquid consequuntur culpa deleniti dolores enim expedita iure laborum libero minus modi necessitatibus perspiciatis quaerat quibusdam saepe vitae, voluptatem!</p>
    <app-button
        v-if="!wasRead"
        color="btn-warning"
        @action="readNews">Прочесть новость
    </app-button>
    <app-news-list></app-news-list>
  </div>
</div>
</template>

<script>
import AppButton from "@/components/AppButton.vue";
import AppNewsList from "@/components/AppNewsList.vue";
export default {
  name: "AppNews.vue",
  emits: {
    'open-news':null,
    'read-news'(id) {
      if(id) {
        return true
      }
      console.warn('Нет параметра id для emit read-news')
      return false
    },
    'no-read-news'(id) {
      if(id) {
        return true
      }
      console.warn('Нет параметра id для emit no-read-news')
      return false
    }
  },
  props: {
    title: {
      type: String,
      required: true
    },
    wasRead: {
      Boolean
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
        return value === true || value === false
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
    },
    readNews() {
      this.$emit('read-news',this.id)
      this.isNewOpen = false
    },
    noReadNews() {
      this.$emit('no-read-news',this.id)
    }
  },
  components: {AppButton, AppNewsList}
}
</script>

<style scoped>
button {
  width: 220px;
  margin: 0 auto;
}
</style>
