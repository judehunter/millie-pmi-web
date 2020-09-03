<template>
  <div class="icon-label">
    <i :class="['bx', icon]" />
    <div v-if="$slots.default">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    icon: {
      type: String,
      default: null
    }
  }
}
</script>

<style lang="scss">
.icon-label {
  @include flex-center(v);
  & > i + div {
    @include flex-center(v);
    margin-left: 7px;
  }
}
</style>
