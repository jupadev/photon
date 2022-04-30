<template>
  <div class="is-flex is-flex-wrap-wrap mt-4">
    <div v-for="image in images" :key="image.id" class="image">
      <nuxt-img
        :src="image.urls.small"
        :alt="image.altDescription"
        loading="lazy"
        class="is-square poster"
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
<style scoped>
.poster {
  object-fit: cover;
  height: 100%;
}
</style>
