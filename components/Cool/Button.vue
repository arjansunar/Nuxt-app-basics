<template>
  <v-btn @click="clicked">cool button</v-btn>
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
