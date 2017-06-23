<template>
  <div class="timeline">
      <router-link to="/"> Retourner sur la page d'accueil</router-link></li>
      <div>Identifié en tant que {{ this.currentUser }}</div>
      <utilisateurs :utilisateurs="utilisateurs" @currentUser="onCurrentUserChange" />
      <feed :tweets="tweets" :loading="isLoading" :currentUser="currentUser" @retweeted="retweet"/>
  </div>
</template>

<script>
import Feed from './Feed'
import Utilisateurs from './Utilisateurs'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  name: 'timeline',
  components: { Feed, Utilisateurs },
  props: [ 'currentUser' ],
  created () {
    this.fetchTweets()
    this.fetchUtilisateurs()
  },
  methods: {
    fetchTweets: function () {
      this.$http.get('http://localhost:8080/list').then(response => {
        this.tweets = response.body
        this.isLoading = false
      }, response => {
        // error callback
      })
    },
    retweet: function (id) {
      for (var i = 0; i < this.tweets.length; i++) {
        if (this.tweets[i].id === id) {
          this.tweets[i].retweeters.push({handle: 'johndoe'})
        }
      }
    },
    fetchUtilisateurs: function () {
      this.$http.get('http://localhost:8080/utilisateurs').then(response => {
        this.utilisateurs = response.body
      }, response => {
        // error callback
      })
    },
    onCurrentUserChange: function (currentUser) {
      this.currentUser = currentUser
    }
  },
  data () {
    return {
      tweets: [],
      isLoading: true
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
