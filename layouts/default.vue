<template>
  <v-app>
    <!-- ヘッダ@スクロール後 -->
    <v-toolbar
      v-if="navView"
      :clipped-left="clipped"
      fixed
      app
      class="header-bar"
      :class="{'header-dummy':!navView}"
    >
      <img src="/img/logo.png" alt="Do's logo" class="logo">
      <nuxt-link to>
        <v-toolbar-title v-text="title"/>
      </nuxt-link>
    </v-toolbar>

    <v-toolbar
      v-if="!navView"
      fixed
      app
      class="header-bar header-dummy"
      style="background-color: rgba(0,0,0,0) !important;"
    ></v-toolbar>

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

    <section class="dummy-form">
      <form name="contact" action="/test" netlify netlify-honeypot="bot-field" hidden>
        <!-- <input type="hidden" name="form-name" value="contact"> -->
        <input type="text" name="name">
        <input type="email" name="email">
        <textarea name="content"></textarea>
      </form>
    </section>
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
      return this.scrollY > 300 - 100 + 44
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
