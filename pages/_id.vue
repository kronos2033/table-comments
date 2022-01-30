<template>
  <div class="index-page">
    <CommentCard :comment="commentParams" />
  </div>
</template>

<script>
export default {
  async asyncData (context) {
    const id = await context.params.id
    const commentParams = await fetch(`https://jsonplaceholder.typicode.com/comments/${id}`).then(res => res.json())
    return { commentParams }
  },
  data () {
    return {
      id: null
    }
  }
}

</script>
