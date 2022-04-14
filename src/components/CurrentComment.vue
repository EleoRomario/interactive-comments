<template>
  <form @submit.prevent="sendComment">
    <div class="current__container">
      <div class="current__user">
        <img
          src="../assets/images/avatars/image-juliusomo.png"
          class="comment__user-avatar"
        />
      </div>
      <div class="comment__textarea">
        <textarea v-model="comment.content" id="" rows="3" class="comment__text"></textarea>
      </div>
      <div class="current__send">
        <button class="button__send">SEND</button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "CurrentComment",
  data(){
    return {      
      comment: {
        content: '',
        createdAt: 'Now',
        score: 0,
        user: {
          username: 'eleoromario',
          image: {
            png: 'images/avatars/image-juliusomo.png',
            webp: 'images/avatars/image-juliusomo.webp',
          },
        },
        replies: [],
      },
    }
  },
  methods: {
    sendComment(){
      this.$emit('add-comment', this.comment);
    }
  }
};
</script>

<style>
</style>