<template>
  <section class="section">
    <FormImage />
    <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <FormResult :images="images" />
  </section>
</template>

<script>
import FormImage from '~/components/FormImage'
import FormResult from '~/components/FormResult'

export default {
  name: 'IndexPage',
  components: {
    FormImage,
    FormResult,
  },

  data() {
    return {
      images: [],
    }
  },
  async fetch() {
    this.images = await fetch('https://serverles-api.jupavar.workers.dev').then(
      (res) => res.json()
    )
  },
  created() {
    this.$nuxt.$on('newResult', (list) => {
      this.images = list
    })
  },
  beforeDestroy() {
    this.$nuxt.$off('newResult')
  },
}
</script>
