<template>
  <div class="comment__container">
    <div class="comment__btns">
      <div class="comment__add button">
        <svg width="11" height="11" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M6.33 10.896c.137 0 .255-.05.354-.149.1-.1.149-.217.149-.354V7.004h3.315c.136 0 .254-.05.354-.149.099-.1.148-.217.148-.354V5.272a.483.483 0 0 0-.148-.354.483.483 0 0 0-.354-.149H6.833V1.4a.483.483 0 0 0-.149-.354.483.483 0 0 0-.354-.149H4.915a.483.483 0 0 0-.354.149c-.1.1-.149.217-.149.354v3.37H1.08a.483.483 0 0 0-.354.15c-.1.099-.149.217-.149.353v1.23c0 .136.05.254.149.353.1.1.217.149.354.149h3.333v3.39c0 .136.05.254.15.353.098.1.216.149.353.149H6.33Z"
            fill="#C5C6EF"
            class="button__icon"
          />
        </svg>
      </div>
      <div class="comment__count">{{ comment.score }}</div>
      <div class="comment__reduce button">
        <svg width="11" height="3" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M9.256 2.66c.204 0 .38-.056.53-.167.148-.11.222-.243.222-.396V.722c0-.152-.074-.284-.223-.395a.859.859 0 0 0-.53-.167H.76a.859.859 0 0 0-.53.167C.083.437.009.57.009.722v1.375c0 .153.074.285.223.396a.859.859 0 0 0 .53.167h8.495Z"
            fill="#C5C6EF"
            class="button__icon"
          />
        </svg>
      </div>
    </div>
    <div class="comment__content">
      <div class="comment__header">
        <div class="comment__user">
          <picture>
            <source
              type="image/webp"
              :src="require(`@/assets/${comment.user.image.webp}`)"
              class="comment__user-avatar"
            />
            <img
              :src="require(`@/assets/${comment.user.image.png}`)"
              class="comment__user-avatar"
            />
          </picture>
          <h4 class="comment__user-name">{{ comment.user.username }}</h4>
          <span class="comment__user-date">{{ comment.createdAt }}</span>
        </div>
        <div class="comment__options">
          <button
            class="comment__delete btn"
            v-if="currentUser.username == comment.user.username"
            @click="this.$emit('delete-comment', comment.id)"
          >
            <svg
              width="12"
              height="14"
              xmlns="http://www.w3.org/2000/svg"
              class="btn__icon"
            >
              <path
                d="M1.167 12.448c0 .854.7 1.552 1.555 1.552h6.222c.856 0 1.556-.698 1.556-1.552V3.5H1.167v8.948Zm10.5-11.281H8.75L7.773 0h-3.88l-.976 1.167H0v1.166h11.667V1.167Z"
                fill="#ED6368"
                class="delete__icon"
              />
            </svg>
            Delete
          </button>
          <button
            @click="editComment(comment)"
            class="comment__edit btn"
            v-if="currentUser.username == comment.user.username"
          >
            <svg
              width="14"
              height="14"
              xmlns="http://www.w3.org/2000/svg"
              class="btn__icon"
            >
              <path
                d="M13.479 2.872 11.08.474a1.75 1.75 0 0 0-2.327-.06L.879 8.287a1.75 1.75 0 0 0-.5 1.06l-.375 3.648a.875.875 0 0 0 .875.954h.078l3.65-.333c.399-.04.773-.216 1.058-.499l7.875-7.875a1.68 1.68 0 0 0-.061-2.371Zm-2.975 2.923L8.159 3.449 9.865 1.7l2.389 2.39-1.75 1.706Z"
                fill="#5357B6"
                class="edit__icon"
              />
            </svg>
            Edit
          </button>
          <button class="comment__reply btn" @click="addReply">
            <svg
              width="14"
              height="13"
              xmlns="http://www.w3.org/2000/svg"
              class="btn__icon"
            >
              <path
                d="M.227 4.316 5.04.16a.657.657 0 0 1 1.085.497v2.189c4.392.05 7.875.93 7.875 5.093 0 1.68-1.082 3.344-2.279 4.214-.373.272-.905-.07-.767-.51 1.24-3.964-.588-5.017-4.829-5.078v2.404c0 .566-.664.86-1.085.496L.227 5.31a.657.657 0 0 1 0-.993Z"
                fill="#5357B6"
                class="reply__icon"
              />
            </svg>
            Reply
          </button>
        </div>
      </div>
      <div class="comment__data">
        <textarea
          class="comment__text-edit"
          v-model="commentEdit.content"
          v-if="editing == comment.id"
        />
        <span v-else class="comment__text">{{ comment.content }}</span>
        <button
          class="button__send"
          v-if="editing == comment.id"
          @click="saveComment"
        >
          UPDATE
        </button>
      </div>
    </div>
  </div>
  <div class="replies__container">
    <div class="replies__lines">
      <div class="replie__line"></div>
    </div>
    <div class="replies__list">
      <ItemReplie
        v-for="replie in comment.replies"
        :key="replie.id"
        :replie="replie"
        :comment="comment"
        :currentUser="currentUser"
        :editing="editing"
        @delete-reply = "deleteReply"
        @add-replyR = "addReply"
      />
    </div>
  </div>
</template>

<script>
import ItemReplie from "./ItemReplie.vue";
export default {
  name: "ItemComment",
  components: {
    ItemReplie,
  },
  props: {
    comment: Object,
    currentUser: Object,
  },
  data() {
    return {
      editing: null,
      commentEdit: this.comment,
      commentReplie: this.comment,
      reply: {
        content:"",
        createdAt: "Now",
        score: 0,
        replyingTo: this.comment.user.username,
        user: {
          image: {
            png: this.currentUser.image.png,
            webp: this.currentUser.image.webp,
          },
          username: this.currentUser.username,
        },
      },
    };
  },
  emits: ["delete-comment", "update-comment"],
  methods: {
    editComment(comment) {
      this.commentText = Object.assign({}, comment);
      this.editing = comment.id;
    },
    saveComment(comment) {
      if (!this.comment.content.length) {
        return;
      }
      this.$emit("update-comment", comment.id, comment);
      this.editing = null;
    },
    addReply() {
      let id = 0;
      if (this.comment.replies.length > 0) {
        id = this.comment.replies[this.comment.replies.length - 1].id + 1;
      }
      this.commentReplie.replies = [
        ...this.commentReplie.replies,
        { id, ...this.reply },
      ];
      this.editing = id;
    },
    deleteReply(id){
      this.commentReplie.replies = this.comment.replies.filter((reply) => reply.id !== id);
    }
  },
};
</script>

<style>
</style>