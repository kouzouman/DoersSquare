<template>
  <section class="area-block">
    <div class="right-line">
      <h3 class="headline mb-2">Contact</h3>

      <div>
        <form v-if="isSubmit === false" @submit.prevent="onSubmit">
          <!-- <input type="text" v-model="name" name="name">
          <input type="email" v-model="email" name="email">
          <textarea v-model="content" name="content"></textarea>
          <button type="submit">送信</button>-->
          <p>
            <label>お名前:
              <v-text-field name="name"></v-text-field>
            </label>
          </p>
          <p>
            <label>メールアドレス:
              <v-text-field name="email"></v-text-field>
            </label>
          </p>
          <p>
            <label>ご用件:
              <v-textarea name="message"></v-textarea>
            </label>
          </p>
          <!-- <div data-netlify-recaptcha="true"></div> -->
          <p>
            <v-btn type="submit">送信</v-btn>
          </p>
        </form>

        <div v-if="isSubmit === true">
          <p>メッセージの投稿ありがとうございます。
            <br>2営業日以内にお返事するように致します。
            <br>しばらくお待ちいただきたく存じます。
          </p>
        </div>
      </div>
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
