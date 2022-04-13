<template>
  <div class="comments__list">
    <ItemComment v-for="item in comments" :key="item.id" :comment="item" />
    <CurrentComment :user="currentUser"/>
  </div>
</template>

<script>
import ItemComment from '@/components/ItemComment.vue';
import CurrentComment from '@/components/CurrentComment.vue';
export default {
  name: 'ListComments',
  components: {
    ItemComment,
    CurrentComment,
  },
  props: {
    comments: Array,
    currentUser: Object
  }
}
</script>

<style>
.comments__list{  
  display: grid;
  grid-template-columns: 1fr;
  grid-auto-rows: 1fr;
  grid-row-gap: 1rem;
  width: 50rem;
  margin-left: auto;
  margin-right: auto;
}
</style>