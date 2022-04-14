<template>  
    <ItemComment v-for="item in comments" :key="item.id" :comment="item" />
</template>

<script>
import ItemComment from "@/components/ItemComment.vue";
export default {
  name: "ListComments",
  components: {
    ItemComment,
  },
  props: {
    comments: Array,
  },
  
};
</script>

<style>
.comments__list {
  display: grid;
  grid-template-columns: 1fr;
  grid-auto-rows: 1fr;
  grid-row-gap: 1rem;
  width: 50rem;
  margin-left: auto;
  margin-right: auto;
}
</style>