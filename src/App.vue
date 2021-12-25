<script>
export default {
  name: 'App',
  data() {
    return {
      quote: null,
      author: null,
    }
  },
  methods: {
    async getRandomQuote() {
      const response = await fetch('https://api.quotable.io/random')
      const responseBody = await response.json()
      this.quote = responseBody.content
      this.author = responseBody.author
    },
  },
  computed: {
    authorLink() {
      return `https://www.google.ca/search?q=${this.author}`
    },
  },
}
</script>

<template>
  <div class="container">
    <h1>Quote generator</h1>
    <button @click="getRandomQuote">Generate random quote</button>
    <div class="quote-card" v-if="quote">
      <h2 v-show="quote" class="quote">
        {{ quote }}
      </h2>
      <h3 class="author" v-if="author">
        <a :href="authorLink" target="_blank"> — {{ author }} </a>
      </h3>
    </div>
  </div>
</template>

<style lang="scss">
@import './styles/normalize.css';

@import url('https://fonts.googleapis.com/css2?family=Merriweather:wght@400;700&display=swap');

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 0 auto;
  max-width: 720px;
  padding: 48px;
  font-family: 'Merriweather', serif;

  h1 {
    margin-bottom: 32px;
    font-weight: 700;
    font-size: 40px;
  }
}

.quote-card {
  display: flex;
  margin-top: 48px;
  width: 100%;
  height: 320px;
  padding: 24px;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border-radius: 12px;
  border: 1px solid #e7e7e9;

  .quote {
    padding: 0 24px;
    line-height: 32px;
    font-weight: 400;
    text-align: center;
    margin-top: auto;
    transition: 400ms opacity;
  }

  .author {
    font-style: italic;
    align-self: flex-end;
    margin-top: auto;
  }
}
</style>
