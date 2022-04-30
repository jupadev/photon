<template>
  <div class="is-flex is-flex-wrap-wrap mt-4">
    <div v-for="image in images" :key="image.id">
      <nuxt-img
        :src="image.urls.thumb"
        :alt="image.altDescription"
        loading="lazy"
        class="image"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'FormResult',
  props: {
    images: {
      type: Array,
      required: true,
    },
  },
}
</script>
