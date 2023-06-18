<template>
  <div
      class="form-control"
      :class="{invalid:error}">
    <label class="form-label" :for="id">{{ label }}</label>
    <input
        class = "form-control"
        :class = margin
        :placeholder = "placeholder"
        :id = "id"
        :value="modelValue"
        :type="type"
        :max="max"
        @input="change"
    >
    <small v-if = "error">{{ error }}</small>
  </div>
</template>

<script>
export default {
  emits: ['update:modelValue'],
  name: "AppInput.vue",
  props: {
    margin: {
      type:String,
      default: '',
      validator(value) {
        return ['mb-3'].includes(value)
      }
    },
    type: String,
    modelValue: {
      type: [String, Number]
    },
    placeholder: String,
    error: String,
    label: String,
    max: String
  },
  methods: {
    change(event) {
      this.$emit('update:modelValue', event.target.value)
    }
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
