<template>
  <h2>Пост с id: {{ id }}</h2>
</template>

<script>
export default {
  async asyncData (context) {
    const id = await context.params.id
    return { id }
  },
  data: () => ({
    id: null
  })
}
</script>

<style scoped>

</style>
