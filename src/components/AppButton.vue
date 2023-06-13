<template>
<button class="btn mb-2 mt-1" :class="color"  @click="$emit('action')"><slot/></button>
</template>

<script>
export default {
  name: "app-button",
  emits:['action'],
  props: {
    color: {
      type:String,
      default:'',
      validator(value) {
        return ['', 'btn-success', 'btn-secondary', 'btn-warning'].includes(value)
      }
    },
  }
}
</script>

<style scoped>

</style>
