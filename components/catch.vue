
<script>
export default {
  props: ['visible']
}
</script>



<template>
  <section class="catch">
    <div v-if="visible">
      <h2 class="display-3 text-xs-center">
        <img src="/img/logo.png" alt="Do's logo" class="logo">
        <span class="biz-name">DoersSquare</span>
      </h2>
      <v-divider dark></v-divider>
      <div class="catch-copy display-1 text-xs-center">毎日の1時間を5分に縮めるご提案</div>
    </div>
  </section>
</template>

<style lang="sass" scoped>
.catch 
  background-color: #17224c
  width: 100%
  min-height: 300px
  padding-top: 55px
  color: #ffffff
  .biz-name
    vertical-align: super
  .catch-copy
    margin-top: 20px

.logo
    width: 75px

</style>
