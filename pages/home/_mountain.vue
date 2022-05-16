<template>
  <v-container>
    <h2 v-if="$fetchState.pending">loading...</h2>
    <div v-else>
      <div class="d-flex align-center justify-space-between">
        <h2 class="">{{ mountain.title }} ({{ mountain.continent }})</h2>
        <nuxt-link to="/home" class="nuxt-link">
          <v-btn>Home</v-btn>
        </nuxt-link>
      </div>
      <span class="text-subtitle-2">&gt; {{ mountain.height }}</span>
      <div class="">
        <img
          :src="mountain.image"
          :alt="mountain.title"
          height="200"
          width="400"
        />
      </div>
      <p class="text-overline">{{ mountain.description }}</p>
    </div>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      mountain: [],
    }
  },
  async fetch() {
    const path = this.$route.query.path
    this.mountain = await fetch(`https://api.nuxtjs.dev/${path}`).then((res) =>
      res.json()
    )
  },
}
</script>

<style scoped>
img {
  object-fit: cover;
}
.nuxt-link {
  text-decoration: none;
}
</style>
