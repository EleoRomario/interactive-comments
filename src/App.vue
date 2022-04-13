<template>
  <ListComments :comments="comments" :currentUser="currentUser"/>
</template>

<script>
import ListComments from '@/components/ListComments.vue';
import data from '@/assets/data/data.json';

export default {
  name: 'App',
  components: {
    ListComments,
  },
  data () {
    console.log(data.comments);
    return {
      currentUser: data.currentUser,
      comments: data.comments,
    }
  },
  computed: {
  }
}
</script>

<style>
@import './assets/css/style.css'
</style>
