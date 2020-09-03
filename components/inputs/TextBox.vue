<template>
  <textarea
    class="text-box"
    rows="4"
    :value="value"
    @input="$emit('update:value', $event.target.value)"
  />
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
.text-box {
  border-bottom: 2px solid #bbb;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  transition: .2s border-color linear;
  padding: .4em .6em;
  background: #fafafa;
  max-width: 100%;
  min-width: 100%;
  min-height: 50px;

  &:hover {
    border-bottom: 2px solid black;
  }

  &:focus {
    border-bottom: 2px solid $primary;
  }
}
</style>
