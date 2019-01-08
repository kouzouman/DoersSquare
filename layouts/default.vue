<template>
  <v-app>
    <!-- ヘッダ@スクロール後 -->
    <v-toolbar v-if="navView" :clipped-left="clipped" fixed app class="header-bar">
      <img src="/img/logo.png" alt="Do's logo" class="logo">
      <nuxt-link to>
        <v-toolbar-title v-text="title"/>
      </nuxt-link>
    </v-toolbar>

    <v-content class="content-area">
      <!-- ヘッダ@スクロール前 -->
      <catch visible="!navView"></catch>
      <v-container>
        <nuxt/>
      </v-container>
    </v-content>
    <v-footer :fixed="fixed" app>
      <span>&copy; 2019～</span>
    </v-footer>
  </v-app>
</template>

<script>
import Catch from '../components/catch'

export default {
  components: {
    catch: Catch
  },
  data() {
    return {
      clipped: false,
      fixed: false,
      items: [
        { icon: 'apps', title: 'Welcome', to: '/' },
        { icon: 'bubble_chart', title: 'Inspire', to: '/inspire' }
      ],
      miniVariant: false,
      right: true,
      title: 'DoersSquare',

      //  追加分  ------------
      scrollY: 0
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.scrollY = window.scrollY
    }
  },
  computed: {
    navView: function() {
      return this.scrollY > 300 - 56
    }
  }
}
</script>

<style lang="sass">

// 定義    ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー
$HEADER-COLOR: #17224c
$BACKGROUND-COLOR: #FFFFFF

$TEXT-COLOR: #17224c
$DARK-TEXT-COLOR: #FFFFFF

</style>
