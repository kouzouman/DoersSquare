<template>
  <v-layout column justify-center>
    <fadein>
      <about></about>
    </fadein>
    <fadein>
      <corresponding-area></corresponding-area>
    </fadein>
    <fadein>
      <profile></profile>
    </fadein>
    <fadein>
      <mail-form></mail-form>
    </fadein>
    <div class="under"></div>
  </v-layout>

  <!-- <section></section> -->
</template>

<script>
import About from '../components/about'
import CorrespondingArea from '../components/corresponding-area'
import Profile from '../components/profile'
import MailForm from '../components/mail-form'
import FadeIn from '../components/slot/fadein'

export default {
  components: {
    about: About,
    'corresponding-area': CorrespondingArea,
    profile: Profile,
    fadein: FadeIn,
    'mail-form': MailForm
  }
}
</script>

<style lang="sass" scoped>
.under
  height : 200px
</style>
