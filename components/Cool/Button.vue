<template>
  <button @click="clicked">cool button</button>
</template>

<script>
export default {
  methods: {
    clicked() {
      this.$emit('clicked')
    },
  },
}
</script>
