<template>
  <input
    type="text"
    class="text-input"
    :value="value"
    @input="$emit('update:value', $event.target.value)"
  >
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss">
.text-input {
  border-bottom: 2px solid #bbb;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  transition: .2s all linear;
  padding: .4em .6em;
  background: #fafafa;

  &:hover {
    border-bottom: 2px solid black;
  }

  &:focus {
    border-bottom: 2px solid $primary;
  }
}
</style>
