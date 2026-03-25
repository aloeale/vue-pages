<template>
  <div class="container">
    <h1>TODAY'S QUOTE</h1>

    <p v-if="loading">Loading...</p>

    <h3 v-if="quote">
      "{{ quote }}"
    </h3>

    <p class="author" v-if="author">
      - {{ author }}
    </p>

    <button @click="getQuote">Get New Quote</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',

  data() {
    return {
      quote: '',
      author: '',
      loading: false
    }
  },

  methods: {
    async getQuote() {
      this.loading = true

      try {
        const response = await axios.get(
          'https://quotes15.p.rapidapi.com/quotes/random/?language_code=en',
          {
            headers: {
              'x-rapidapi-host': 'quotes15.p.rapidapi.com',
              'x-rapidapi-key': '7a0fe8ba65msh1cb4a5326e438cbp197578jsnc25eae1a1cca'
            }
          }
        )

        this.quote = response.data.content
        this.author = response.data.originator.name

      } catch (error) {
        console.error('Error:', error)
        this.quote = 'Oops! Something went wrong.'
        this.author = ''
      }

      this.loading = false
    }
  },

  mounted() {
    this.getQuote()
  }
}
</script>

<style>
<style>
.container {
  text-align: center;
  font-family: Arial, sans-serif;
  margin-top: 50px;
  background-color: rgb(247, 226, 199);
  height: 100vh;
  padding-top: 5%;
  border: 2px solid rgb(194, 4, 105);
}

h1 {
  color: rgb(194, 4, 105);
}

h3, h4 {
  color: rgb(84, 38, 62);
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 16px;
  background-color: rgb(194, 4, 105);
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: rgb(150, 3, 80);
}

.author {
  font-style: italic;
  color: #555;
  margin-top: 5px;
}
</style>
