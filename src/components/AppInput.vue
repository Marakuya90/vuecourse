<template>
  <div
      class="form-control"
      :class={invalid:error}>
    <label class="form-label" :for="id">{{ label }}</label>
    <input
        type = "text"
        class = "form-control mb-3"
        :placeholder = "placeholder"
        :id = "id"
        v-model.trim = "name"
    >
    <small v-if = "error">{{ error }}</small>
  </div>
</template>

<script>
export default {
  name: "AppInput.vue",
  props: {
    placeholder: String,
    error: String,
    label: String,
  },
  data() {
    return {
      id: 'input-' + Math.random()
    }
  }
}
</script>

<style scoped>

</style>
