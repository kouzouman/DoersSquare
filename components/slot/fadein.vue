<template>
  <div>
    <transition name="fade">
      <slot v-if="visible"></slot>
    </transition>
  </div>
</template>


<script>
export default {
  data: () => ({
    visible: false,
    interval: null
  }),
  methods: {
    handleScroll() {
      if (!this.visible) {
        try {
          var top = this.$el.getBoundingClientRect().top
          this.visible = top < window.innerHeight + 100
          // clearInterval(this.interval)
        } catch (e) {}
      }
    }
  },
  created() {
    try {
      this.interval = setInterval(() => {
        this.handleScroll()
      }, 500)
    } catch (e) {}
  },
  destroyed() {
    try {
      if (!!window) {
        window.removeEventListener('scroll', this.handleScroll)
      }
    } catch (e) {}
  }
}
</script>

<style lang="sass" scoped>


.fade-enter-active,
.fade-leave-active 
  transition: opacity 1s


.fade-enter,
.fade-leave-to 
  opacity: 0


</style>
