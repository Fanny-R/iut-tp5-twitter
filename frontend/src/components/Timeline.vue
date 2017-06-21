<template>
  <div class="timeline">
      <ul>
       <li v-for="tweet in tweets"> {{ tweet.auteur }} {{ tweet.contenu }}</li>
      </ul>
      <router-link to="/"> Retourner sur la page d'accueil</router-link></li>
  </div>
</template>

<script>
var tweet1 = {auteur: 'Bob', contenu: 'Blabla'}
var tweet2 = {auteur: 'Roger', contenu: 'Blublu'}
var tweet3 = {auteur: 'Simone', contenu: 'Blibli'}
export default {
  name: 'timeline',
  data () {
    return {
      tweets: [tweet1, tweet2, tweet3]
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
