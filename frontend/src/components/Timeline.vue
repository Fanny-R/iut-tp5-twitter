<template>
  <div class="timeline">
      <ul>
       <li v-for="tweet in tweets">
          <tweet :tweet="tweet"/>
       </li>
      </ul>
      <router-link to="/"> Retourner sur la page d'accueil</router-link></li>
  </div>
</template>

<script>
import Tweet from './Tweet'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

fetch
export default {
  name: 'timeline',
  data () {
    return {
      tweets: []
    }
  },
  components: { Tweet },
  created () {
    this.fetchTweets()
  },
  methods: {
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
      }, response => {
        // error callback
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
