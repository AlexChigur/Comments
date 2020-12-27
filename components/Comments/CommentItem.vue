<template>
  <div class="comment-item">
    <div class="comment-item__content">
      <div class="comment-item__content__id"> User id: {{ comment.id }}</div>
      <div class="comment-item__content__text" v-if="!isEditable">{{ comment.text }}</div>
      <div v-else class="comment-item__content__editable">
        <textarea :value="comment.text" @input="changeText($event)"/>
        <div class="editable__buttons">
          <BaseButton type="s" button-text="Save" @click="setComment(comment.id, comment.text)"/>
          <BaseButton class="editable__buttons__cancel" type="s" button-text="Cancel" @click="isEditable = !isEditable"/>
        </div>
      </div>
      <div class="comment-item__content__settings" v-if="!isAddSubComment && !isEditable">
        <BaseButton type="s" button-text="Reply" class="settings__add-reply" @click="isAddSubComment = !isAddSubComment"/>
        <BaseButton type="s" button-text="Edit" class="settings__edit" @click="isEditable = !isEditable"/>
        <BaseButton type="s" button-text="Delete" class="settings__delete" @click="deleteComment"/>
      </div>
    </div>
    <ul class="comment-item__subcomments">
      <CommentItem
        v-for="(subComment, index) in comment.subComments"
        :comment="subComment"
        :key="subComment.id"
        :parentItem="comment"
        :index="index"
      ></CommentItem>
    </ul>
    <div class="comment-item__create-comment" v-if="isAddSubComment">
      <div class="comment-item__create-comment__text-area">
        <textarea v-model="message" placeholder="Enter your comment"/>
      </div>
      <div class="comment-item__create-comment__add-button">
        <BaseButton type="m" button-text="Leave a comment" @click="addNewSubComment"/>
        <BaseButton class="add-button__cancel" type="m" button-text="Cancel" @click="isAddSubComment = !isAddSubComment"/>
      </div>
    </div>
  </div>
</template>

<script>
  import { ID } from '../../helpers/generateId'
  import BaseButton from "../Base/BaseButton";
  export default {
    name: 'CommentItem',
    components: {BaseButton},
    data() {
      return {
        isAddSubComment: false,
        isEditable: false,
        message: null,
        editedComment: null
      }
    },
    props: {
      comment: {
        type: Object,
        default: null
      },
      index: {
        type: Number,
        required: true
      },
      parentItem: {
        required: false
      }
    },
    computed: {

    },
    methods: {

      addNewSubComment() {
        const subCommit = {
          text: this.message,
          id: ID(),
          subComments: []
        }
        this.comment.subComments.push(subCommit)
        this.isAddSubComment = false
        this.message = null
      },

      deleteComment() {

        if (this.parentItem) {
          this.parentItem.subComments.splice(this.index, 1);
          return;
        }
        this.$emit('deleteComment', this.index)
      },

      setComment() {
        this.comment.text = this.editedComment
        this.isEditable = false
      },
      changeText(event) {
        this.editedComment = event.target.value
      }
    },
  }
</script>

<style lang="scss" scoped>

  .comment-item {
    width: 100%;
    .comment-item__content {
      position: relative;
      width: 100%;
      height: 100px;
      border: 2px black solid;
      margin: 60px 0;

      .comment-item__content__text {
        background-color: transparent;
        border: none;
        color: black;
        padding: 5px 0 0 15px;
      }

      .comment-item__content__id {
        padding: 5px;
      }

      .comment-item__content__settings {
        position: absolute;
        display: flex;
        justify-content: flex-end;
        right: 0;
        bottom: -26px;

        .settings__add-reply,
        .settings__delete,
        .settings__edit {
          margin-left: 10px;
        }
      }

      .comment-item__content__editable {

        .editable__buttons {
          margin-right: 15px;
          display: flex;
          justify-content: flex-end;

          .editable__buttons__cancel {
            margin-left: 10px;
          }
        }

        textarea {
          resize: none;
          width: 100%;
          box-sizing: border-box;
        }
      }
    }
    .comment-item__subcomments {
      padding-left: 20px;
    }

    .comment-item__create-comment {

      .comment-item__create-comment__add-button {
        display: flex;
        justify-content: flex-end;

        .add-button__cancel {
          margin-left: 10px;
        }
      }
      .comment-item__create-comment__text-area {
        textarea {
          resize: none;
          width: 100%;
          box-sizing: border-box;
          height: 60px;
        }
      }
    }
  }

</style>
