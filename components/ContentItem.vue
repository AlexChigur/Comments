<template>
  <div class="content">
    <div class="content__post">
      Hello dude
    </div>
    <CommentsList/>
  </div>

</template>

<script>
import CommentsList from "./Comments/CommentsList";
import BaseButton from "./Base/BaseButton";
export default {
  data() {
    return {
      isAddComment: false,
    }
  },
  components: {
    BaseButton,
    CommentsList,

  },
}
</script>

<style lang="scss" scoped>
  .content {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    width: fit-content;

    .content__post {
      width: 600px;
      height: 200px;
      border: solid 2px black;
    }

    .content__comment-button {
      margin-left: auto;
    }
  }


</style>
