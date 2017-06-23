<template>
  <div class="tweet">
    <div>
      <strong> {{ tweet.auteur.prenom }} {{ tweet.auteur.nom }} </strong> <span class=handle> @{{ tweet.auteur.handle }} </span> - {{ moment(tweet.date).fromNow() }}
    </div>
    <div>
      {{ tweet.contenu }}
    </div>
    <div>
      <ul>
        <li class=button>
          <icon name="reply"/> {{ tweet.retweeters.length }}
          <a @click="retweet(tweet.id)">
            <icon name="retweet"/>
          </a>
          <icon name="heart"/>
          <icon name="envelope"/>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'
import moment from 'moment'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)

export default {
  created () {
    moment.locale('fr')
  },
  name: 'tweet',
  props: [ 'tweet' ],
  components: { Icon },
  methods: {
    moment: function (date) {
      return moment(date)
    },
    retweet: function (id) {
      var formData = new FormData()
      formData.append('utilisateur', 'johndoe')
      formData.append('tweet', id)
      this.$http.post('http://localhost:8080/retweet', formData, {responseType: 'text'}).then(response => {
        this.$emit('retweeted', id)
      })
    }
  }
}
</script>

<style scoped>
  li.button {
   display: inline-block;
  }

  a {
   color: #42b983;
  }

  span.handle {
   color: gray;
  }
</style>
