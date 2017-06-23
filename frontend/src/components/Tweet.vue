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
          <icon name="reply"/>
          <icon name="retweet"/>
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
