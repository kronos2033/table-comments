<template>
  <div>
    <div class="comment">
      <span class="comment__info">Comment №{{ comment.id }} for post №{{ comment.postId }}</span>
      <h2 class="comment__title">
        {{ capitalizeFirstChar(comment.name) }}
      </h2>
      <p class="comment__body">
        {{ capitalizeFirstChar(comment.body) }}
      </p>
      <p class="comment__user">
        {{ comment.email }}
      </p>
    </div>
    <button class="btn" @click="$router.back()">
      Вернуться к списку комментарией
    </button>
  </div>
</template>

<script>
export default {
  props: {
    comment: {
      type: Object,
      default: null
    }
  },
  methods: {
    capitalizeFirstChar (text) {
      return text.charAt(0).toUpperCase() + text.slice(1)
    }
  }
}

</script>

<style scoped>
.comment {
  border-radius: 4px;
  background: #fff;
  box-shadow: 0 6px 10px rgba(0,0,0,.08), 0 0 6px rgba(0,0,0,.05);
  max-width: 900px;
  margin: 10px auto;
  padding: 20px;
}

.comment:hover{
  box-shadow: 0 10px 20px rgba(0,0,0,.12), 0 4px 8px rgba(0,0,0,.06);
}
.comment__info {
  color: #44475C;
  font-size: 14px;
}

.comment__title {
  font-size: 30px;
}

.comment__body {
  font-size: 24px;
}

.comment__user {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  font-size: 14px;
  margin: 0
}
.comment__user::before {
  content: url("assets/user-avatar.png");
}
</style>
