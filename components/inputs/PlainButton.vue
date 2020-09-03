<template>
  <button
    :class="['plain-button', round && 'plain-button--round']"
    :style="[{color: textColor}, color && {backgroundColor: color}]"
    @click="$emit('click')"
  >
    <slot />
  </button>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      default: ''
    },
    round: Boolean
    // size: null
  },
  computed: {
    textColor() {
      if (!this.color) return 'white';
      const hexcolor = this.color.replace('#', '');
      const r = parseInt(hexcolor.substr(0, 2), 16);
      const g = parseInt(hexcolor.substr(2, 2), 16);
      const b = parseInt(hexcolor.substr(4, 2), 16);
      const yiq = ((r * 299) + (g * 587) + (b * 114)) / 1000;
      return (yiq >= 200) ? 'black' : 'white';
    }
  }
}
</script>

<style lang="scss">
.plain-button {
  padding: .4em .9em;
  background-color: $primary;
  border-radius: 4px;

  &--round {
    border-radius: 100px;
  }
}
</style>
