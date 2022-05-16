<template>
  <v-container class="d-flex flex-column align-center justify-center">
    <div class="text-h1">home</div>
    <nuxt-link to="/">index</nuxt-link>

    <div>
      <p v-if="$fetchState.pending">Fetching mountains...</p>
      <p v-else-if="$fetchState.error">An error occurred :(</p>
      <div v-else>
        <h1 class="text-overline">Nuxt Mountains</h1>
        <CoolButton @clicked="clicked" />

        <ul>
          <li v-for="(mountain, i) of mountains" :key="i">
            <NuxtLink :to="`${mountain.title}`">
              <h2 class="text-h5">{{ mountain.title }}</h2>
              <span>{{ mountain.height }}</span>
              <div class="">
                <img
                  :src="mountain.image"
                  :alt="mountain.title"
                  height="400"
                  width="400"
                />
              </div>
            </NuxtLink>
          </li>
        </ul>
      </div>
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'Home',
  // exposes variables to the templates
  data() {
    return {
      mountains: [],
      title: 'Mountains | home',
    }
  },
  // does the api requests to fetch external resources
  async fetch() {
    this.mountains = await fetch('https://api.nuxtjs.dev/mountains').then(
      (res) => res.json()
    )
  },
  // head method injects metadata to the head component in html
  head() {
    return {
      title: this.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'description',
          name: 'description',
          content: 'My custom description',
        },
      ],
    }
  },
  methods: {
    clicked() {
      alert('Button clicked')
    },
  },
}
</script>

<style scoped>
img {
  object-fit: cover;
  aspect-ratio: 16/9;
}
</style>
