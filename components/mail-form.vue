<template>
  <section class="area-block">
    <div class="left-line">
      <h3 class="headline mb-2">Contact</h3>

      <div>
        <form v-if="isSubmit === false" @submit.prevent="onSubmit">
          <input type="text" v-model="name" name="name">
          <input type="email" v-model="email" name="email">
          <textarea v-model="content" name="content"></textarea>
          
          <button type="submit">送信</button>
        </form>

        <div v-if="isSubmit === true">
          <p>サンクス</p>
        </div>
      </div>

      <!-- 
      <div>
        <form
          name="contact"
          netlify-honeypot="bot-field"
          action="thank-you"
          netlify
          data-netlify="true"
          method="post"
        >
          <input type="hidden" name="form-name" value="contact">
          <p class="hidden" style="display: none;">
            <label>Don’t fill this out:
              <input name="bot-field">
            </label>
          </p>
          <p>
            <label>Your Name:
              <v-text-field name="name"></v-text-field>
            </label>
          </p>
          <p>
            <label>Your Email:
              <v-text-field name="email"></v-text-field>
            </label>
          </p>
          <p>
            <label>Message:
              <v-textarea name="message"></v-textarea>
            </label>
          </p>
          <div data-netlify-recaptcha="true"></div>
          <p>
            <v-btn type="submit">Send</v-btn>
          </p>
        </form>
      </div>-->
    </div>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      name: '',
      email: '',
      content: '',
      isSubmit: false
    }
  },
  methods: {
    onSubmit() {
      console.log('form-submit')
      const params = new URLSearchParams()

      params.append('form-name', 'contact') // Forms使うのに必要

      params.append('name', this.name)
      params.append('email', this.email)
      params.append('content', this.content)

      axios.post('/', params).then(() => {
        this.isSubmit = true
      })
    }
  }
}
</script>
