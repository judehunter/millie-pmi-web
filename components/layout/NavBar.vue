<template>
  <nav class="nav-bar">
    <div>
      <svg viewBox="0 0 140 32" :class="[white && 'white']">
        <path d="M40.5 31.3h-7.4l-3.6-21.1-5.9 21.1H17l-6-21.1-3.6 21.1H0L5.9.7h8l6.4 21.5L26.6.7h8zM45.6.7h6.7v30.6h-6.7zm14.3 30.6V.7h6.7v24.5h11v6.1zm24.1 0V.7h6.7v24.5h10.9v6.1zM108 .7h6.7v30.6H108zm32 24.5v6.1h-17.7V.7H140v6.1h-11v6.1h10.6V19H129v6.2z" />
      </svg>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    white: Boolean
  },
  data() {
    return {
      isScrolled: false,
      isMobileOpen: true
    }
  },
  // improve this performance-wise
  beforeMount () {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy () {
    window.removeEventListener('scroll', this.handleScroll);
  },
  mounted() {
    this.handleScroll();
  },
  methods: {
    handleScroll () {
      const scroll = window.pageYOffset || document.documentElement.scrollTop;
      if (scroll > this.scrolledThreshold) this.isScrolled = true;
      else if (scroll < this.scrolledThreshold / 2) this.isScrolled = false;
    }
  }
}
</script>

<style lang="scss" scoped>
.nav-bar {
  text-align: center;
  position: static;
  width: 100%;
  z-index: 99999999;
  transition: .15s all ease-in-out;;

  padding-top: 30px;
  padding-bottom: 30px; //50
}

svg {
  fill: black;
  max-width: 15%;
  min-width: 100px;

  &.white {
    fill: white;
  }
}
</style>
