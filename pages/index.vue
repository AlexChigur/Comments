<template>
  <div class="container">
    <ContentItem/>
  </div>
</template>

<script>
import ContentItem from "../components/ContentItem";

export default {
  components: {
    ContentItem
  },
}
</script>

<style lang="scss">

  .container {
    height: 100%;
    display: flex;
    justify-content: center;
  }

</style>
