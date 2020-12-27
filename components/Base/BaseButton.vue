<template>
  <div>
    <button :class="[`base-button-${type}`, 'base-button']" @click="onClick">{{ buttonText }}</button>
  </div>
</template>

<script>
  export default {
    props: {
      buttonText: {
        type: String,
      },
      type: {
        type: String,
        default: 'xl'
      }
    },
    methods: {
      onClick(event) {
        this.$emit('click', event)
      }
    }
  }
</script>

<style lang="scss" scoped>

  .base-button {
    background-color: #25b0ff;
    border-radius: 8px;
    color: White;
    border: none;
    cursor: pointer;

    &:hover {
      background-color: #279ce0;
    }
  }

  .base-button-xl {
    width: 150px;
    height: 40px;
    font-size: 16px;
  }

  .base-button-m {
    width: 150px;
    height: 30px;
    font-size: 14px;
  }

  .base-button-s {
    width: 100px;
    height: 20px;
    font-size: 12px;
  }

</style>
