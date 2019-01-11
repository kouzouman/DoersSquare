<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <div class="text-xs-center"></div>
    </v-flex>

    <about></about>
    <corresponding-area></corresponding-area>
  </v-layout>
</template>

<script>
import About from '../components/about'

import CorrespondingArea from '../components/corresponding-area'

export default {
  components: {
    about: About,
    'corresponding-area': CorrespondingArea
  }
}
</script>
