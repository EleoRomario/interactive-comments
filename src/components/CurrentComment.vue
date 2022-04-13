<template>
  <div class="current__container">
    <div class="current__user">
      <img :src="require(`@/assets/${user.image.png}`)" class="comment__user-avatar">
    </div>
    <div class="comment__textarea">
      <textarea name="" id="" rows="3" class="comment__text"></textarea>
    </div>
    <div class="current__send">
      <div class="button__send">SEND</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CurrentComment",
  props: {
    user: Object,
  }
}
</script>

<style>

</style>