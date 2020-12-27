<template>
 <div class="comments-list">
   <div class="comments-list__comments">
     <CommentItem
       v-for="(comment, index) in comments"
       :comment="comment"
       :key="comment.id"
       :index="index"
       @deleteComment="deleteComment"
     />
     <div class="comments__create-comment" v-if="isAddComment">
       <div class="comments__create-comment__text-area">
         <textarea v-model="message" placeholder="Enter your comment"></textarea>
       </div>
       <div class="comments__create-comment__add-button">
         <BaseButton @click="addNewComment" button-text="Leave a comment"/>
       </div>
     </div>
  </div>
 <div v-if="!isAddComment" class="comments-list__add-comment">
   <BaseButton @click="isAddComment = !isAddComment" button-text="Add comment"/>
 </div>
 </div>
</template>

<script>
import CommentItem from "./CommentItem";
import {ID} from "../../helpers/generateId";
import BaseButton from "../Base/BaseButton";
export default {

  data() {
    return {
      isAddComment: false,
      message: null,
      comments: []
    }
  },

  components: {
    BaseButton,
    CommentItem
  },

  methods: {
    addNewComment() {
      const newComment = {
        id: ID(),
        text: this.message,
        subComments: []
      }
      this.comments.push(newComment)
      this.message = null
      this.isAddComment = false
    },
    deleteComment(index) {
      this.comments.splice(index, 1)
    }
  }

}
</script>

<style lang="scss" scoped>

  .comments-list {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;

    .comments-list__comments {
      width: 100%;
      .comments__create-comment {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        margin-top: 12px;

        .comments__create-comment__text-area {
          width: 400px;

          textarea {
            resize: none;
            width: 100%;
            box-sizing: border-box;
            height: 60px;
          }
        }
        .comments__create-comment__add-button {

        }
      }
    }
    .comments-list__add-comment {
      margin: 12px 0 0 auto;
    }
  }
</style>
