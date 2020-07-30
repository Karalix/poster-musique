<template>
  <div class="services">
    <Header :title="ownEvent.name" :img="ownEvent.image" :date="date" :icon="2"></Header>
    <!--<EventVignette :eventobj="item" v-for="item of ownEvents" :key="item.name"></EventVignette>-->
    <h2>Autour de l'événement</h2>
    <ServiceVignette :eventobj="item" v-for="item of localServices" :key="item.name"></ServiceVignette>
    <div class="dual-container">
       <div class="half-width-container">
        <h2>Autour du rap</h2>
        <ArticleVignette v-for="article of localArticles" :key="article.name" :article="article"></ArticleVignette>
      </div>
      <div class="half-width-container">
        <h2>Vos questions</h2>
        <QAVignette v-for="qa of localGuichet" :key="qa.q" :qa="qa"></QAVignette>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import ArticleVignette from '@/components/ArticleVignette.vue'
import ServiceVignette from '@/components/ServiceVignette.vue'
import QAVignette from '@/components/QAVignette.vue'

export default {
  name: 'patrimoine',
  components: {
    Header,
    ArticleVignette,
    ServiceVignette,
    QAVignette
  },
  props: [
    'events',
    'services',
    'articles',
    'videos',
    'guichet'
  ],
  methods: {
    relayPopup: function (label) {
      let ag = label
      ag.event = this.ownEvent.name
      this.$emit('popup', ag)
    }
  },
  computed: {
    localGuichet: function () {
      return this.guichet.filter(el => {
        return el.type && el.type === 'local'
      })
    },
    localArticles: function () {
      return this.articles.filter((el) => {
        return el.type && el.type === 'local'
      })
    },
    ownEvent: function () {
      return this.events.filter(el => {
        return el.type && el.type === 'local'
      })[0]
    },
    localServices: function () {
      return this.services.filter(el => {
        return el.type && el.type === 'local'
      })
    },
    localVideos: function () {
      return this.videos.filter(el => {
        return el.type && el.type === 'local'
      })
    },
    date: function () {
      let options = { day: 'numeric', month: 'long' }
      return (new Date(this.ownEvent.date)).toLocaleDateString('fr-FR', options)
    }
  }
}
</script>
