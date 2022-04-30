<template>
  <form
    id="formimage"
    ref="form"
    class="is-flex"
    action="https://vuejs.org/"
    method="post"
    @submit="handleSubmit"
  >
    <div class="is-flex-grow-2">
      <label>
        <input
          id="search"
          v-model="search"
          type="search"
          name="search"
          :placeholder="placeholder"
          class="input"
        />
      </label>
      <ul v-if="errors.length">
        <li v-for="error in errors" :key="error">{{ error }}</li>
      </ul>
    </div>
    <button type="submit" class="button">{{ searchButton }}</button>
  </form>
</template>
<script>
export default {
  name: 'SearchForm',
  props: {
    placeholder: {
      type: String,
      default: 'Search an image',
    },
    searchButton: {
      type: String,
      default: 'Search',
    },
  },
  data() {
    return {
      errors: [],
      search: '',
      images: [],
    }
  },
  methods: {
    async handleSubmit(e) {
      e.preventDefault()
      this.errors = []
      if (!this.search) {
        this.errors.push('search criteria is mandatory')
        return
      }

      const images = await fetch(
        `https://serverles-api.jupavar.workers.dev?query=${this.search}`
      ).then((res) => res.json())
      this.$nuxt.$emit('newResult', images)
    },
  },
}
</script>
