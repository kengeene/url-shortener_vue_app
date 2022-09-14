<template>
  <div class="container">
    <p class="textBox">Insert your URL here:</p>
    <input v-model="originalURL" class="textBox" />
    <button class="textBox" @click="fetchUrl">Convert URL</button>
    <span class="textBox"
      ><a :href="shortenedURL" target="blank">{{ shortenedURL }}</a></span
    >
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    age: {
      type: Number,
      default: 2,
    },
  },
  data() {
    return {
      originalURL: '',
      shortenedURL: '',
    }
  },
  methods: {
    async fetchUrl() {
      const url = new URL('https://t.ly/api/v1/link/shorten')

      const params = {
        api_token: 'V4BVn8jdbCCdWhvqDepu9kvcf0p7kjJQv3bHhsz4eF3vJkhhNrZ71Z4yumuq',
      }
      Object.keys(params).forEach((key) => url.searchParams.append(key, params[key]))

      const headers = {
        'Content-Type': 'application/json',
        Accept: 'application/json',
      }

      let body = {
        long_url: this.originalURL,
        domain: 'https://t.ly/',
        include_qr_code: false,
      }

      const { short_url } = await fetch(url, {
        method: 'POST',
        headers,
        body: JSON.stringify(body),
      }).then((response) => response.json())

      this.shortenedURL = short_url
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin: 0 auto;
  text-align: center;
}
.textBox {
  display: block;
  margin: 0;
}
</style>
