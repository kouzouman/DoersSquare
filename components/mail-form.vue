<template>
  <section class="area-block">
    <div class="left-line">
      <h3 class="headline mb-2">Contact</h3>
      <div>
        <form name="contact" method="POST" data-netlify="true" action="/">
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
          <p>
            <v-btn type="submit">Send</v-btn>
          </p>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
export default {}
</script>
