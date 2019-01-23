<template>
  <section class="area-block">
    <div class="right-line">
      <h3 class="headline mb-2">Contact</h3>

      <div>
        <form v-if="isSubmit === ''" @submit.prevent="onSubmit">
          <p>
            <label>お名前:
              <v-text-field name="name" v-model="name"></v-text-field>
            </label>
          </p>
          <p>
            <label>メールアドレス:
              <v-text-field name="email" v-model="email"></v-text-field>
            </label>
          </p>
          <p>
            <label>ご用件:
              <v-textarea name="message" v-model="content"></v-textarea>
            </label>
          </p>
          <!-- <div data-netlify-recaptcha="true"></div> -->
          <p>
            <v-checkbox :label="`私はロボットではありません`" @click="checkUnrobot" v-model="chkUnrobot"></v-checkbox>
            <span class="hd">
              <input type="checkbox" v-model="dcheck">
            </span>
            <v-btn type="submit">送信</v-btn>
          </p>
        </form>

        <div v-if="isSubmit === 'OK'">
          <p>メッセージの投稿ありがとうございます。
            <br>2営業日以内にお返事するように致します。
            <br>しばらくお待ちいただきたく存じます。
          </p>
        </div>
        <div v-if="isSubmit === 'NG'">
          <p>メッセージの投稿ありがとうございます。
            <br>しかし、申し訳ありません。ロボットでない確認が取れなかったため送信できませんでした。
            <br>操作をゆっくりにして、もう一度投稿いただけませんでしょうか。
            <br>よろしくおねがいします。
          </p>
        </div>
        <div v-if="isSubmit === 'NJPN'">
          <p>メッセージの投稿ありがとうございます。
            <br>しかし、申し訳ありません。現在日本語によるメッセージのみを受け付けております。
            <br>お送りいただいた内容は受信できません。
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
      viewStartTime: new Date(),
      unrobotCheckTime: null,
      chkUnrobot: false,
      dcheck: false,
      isSubmit: ''
    }
  },
  methods: {
    checkUnrobot() {
      const viewedTime = new Date() - this.viewStartTime
      if (viewedTime > 1500) {
        this.unrobotCheckTime = new Date()
      }
      this.chkUnrobot = true
    },
    onSubmit() {
      console.log('form-submit')

      if (!this.content.match(/[亜-熙ぁ-んァ-ヶ]/)) {
        this.isSubmit = 'NJPN'
        return
      }

      if (this.dcheck || this.unrobotCheckTime == null) {
        this.isSubmit = 'NG'
        return
      }
      const sa = new Date() - this.unrobotCheckTime
      if (sa < 300) {
        this.isSubmit = 'NG'
        return
      }

      const params = new URLSearchParams()

      params.append('form-name', 'contact') // Forms使うのに必要

      console.log({
        name: this.name,
        email: this.email,
        content: this.content,
        chkUnrobot: this.chkUnrobot
      })

      params.append('name', this.name)
      params.append('email', this.email)
      params.append('content', this.content)
      // params.append('chkRobot', this.chkUnrobot)

      console.log(params)

      axios.post('/', params).then(() => {
        this.isSubmit = 'OK'
      })
    }
  }
}
</script>

<style>
.hd {
  display: none;
}
</style>
