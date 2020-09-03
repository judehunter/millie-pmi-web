<template>
  <div class="checkbox">
    <div class="checkbox__side">
      <input
        :id="hash"
        type="checkbox"
        :name="hash"
        :checked="value"
        :class="['checkbox__input', disabled && 'disabled']"
        @change="$emit('update:value', !value)"
      >
    </div>
    <component :is="labeled ? 'label' : 'div'" v-if="$slots.default" :for="hash" class="checkbox__content">
      <slot />
    </component>
  </div>
</template>

<script>
export default {
  props: {
    labeled: Boolean,
    disabled: Boolean,
    value: null
  },
  data() {
    return {
      hash: this._uid
    }
  },
  watch: {
    value() {
      this.$emit('update:value', this.value);
    }
  }
}
</script>

<style lang="scss">
.checkbox {
  @include flex-center(v);
  filter: hue-rotate(160deg) brightness(1.7);
  &__side {
    width: 35px;
    &.outdent {
      @media (min-width: 1000px) {
        margin-left: -40px
      }
    }
    & > input {
      margin: 0 3px 0 3px;
      transform: scale(1.3);
    }
  }

  &__content {
    flex-grow: 1;
  }

  &__input.disabled {
    pointer-events: none;
    opacity: .6;
  }
}
</style>
