<template>  
    <ItemComment v-for="item in comments" :key="item.id" :comment="item" :currentUser="currentUser" @delete-comment="deleteComment"/>
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
    currentUser: Object,
  },
  emits: ["delete-comment", "update-comment"],
  methods: {
    deleteComment(id) {
      this.$emit("delete-comment", id);
    },
  },
};
</script>

<style>
.comments__list {
  display: grid;
  grid-template-columns: 1fr;
  grid-row-gap: 1rem;
  width: 50rem;
  margin-left: auto;
  margin-right: auto;
  margin-top: 2rem;
  margin-bottom: 2rem;
}
</style>