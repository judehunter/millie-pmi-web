<template>
  <div class="layout-admin">
    <nav-bar :white="false" />
    <Nuxt />
    <foot />
  </div>
</template>

<style lang="scss">
@import "~/styles/reset.scss";

html {
  font-family: $display-stack;
  line-height: 1.20;
}

.container {
  @include margin-center;
  max-width: 750px;
}

.layout-admin {
  color: black;
}

.padded-container {
  @extend .container;
  @include padded-sides(15px, 30px);
}

h1, h2, h3, h4, h5, h6 {
  font-family: $display-stack;
  // margin-top: .1em;
  // margin-bottom: .1em;
}

.c-primary {
  color: $primary;
}
.w-500 {
  font-weight: 500;
}
.w-600 {
  font-weight: 600;
}
</style>
