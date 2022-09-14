<template>
  <div class="container">
    <p>Insert your URL here:</p>
    <input v-model="originalURL" class="textbox" />
    <button v-loading="loading" @click="fetchUrl">Convert URL</button>
    <span class="results">
      <a :href="shortenedURL" target="blank" class="result-test">{{ shortenedURL }}</a>
    </span>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      originalURL: '',
      shortenedURL: '',
      loading: false,
    }
  },
  methods: {
    async fetchUrl() {
      this.loading = true
      const url = new URL('https://t.ly/api/v1/link/shorten')

      const params = {
        api_token: 'f4h4fA9V6fMNPGCy8Oea6GQTgiIHSbat5jJoBXDAUV62TU2BbKU9hiUzAgsP',
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
      this.loading = false
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin: 0 auto;
  text-align: center;
  width: 100%;
}
.textbox {
  margin: 20px;
}
.results {
  display: block;
}
</style>
