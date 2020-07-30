<template>
  <div class="showcase">
    <Header :title="ownEvent.name" :img="ownEvent.image" :date="date" :icon="0"></Header>
    <h2>Autour de l'événement</h2>
    <ServiceVignette :eventobj="item" v-for="item of showcaseServices" :key="item.name"></ServiceVignette>
    <div class="dual-container">
      <div class="half-width-container">
        <h2>A redécouvrir</h2>
        <ArticleVignette v-for="article of showcaseArticles" :key="article.name" :article="article"></ArticleVignette>
      </div>
      <div class="half-width-container">
        <h2>Explorer ces contenus</h2>
        <p class="rdv-tablet">Rendez-vous sur la tablette</p>
        <img src="/img/seetablet.svg"/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import ServiceVignette from '@/components/ServiceVignette'
import ArticleVignette from '@/components/ArticleVignette'

export default {
  name: 'showcase',
  components: {
    Header,
    ServiceVignette,
    ArticleVignette
  },
  props: [
    'services',
    'articles',
    'events'
  ],
  methods: {
    relayPopup: function (label) {
      let ag = label
      ag.event = this.ownEvent.name
      this.$emit('popup', ag)
    }
  },
  computed: {
    showcaseServices: function () {
      return this.services.filter((el) => {
        return el.type && el.type === 'showcase'
      })
    },
    showcaseArticles: function () {
      return this.articles.filter((el) => {
        return el.type && el.type === 'showcase'
      })
    },
    ownEvent: function () {
      return this.events.filter(el => {
        return el.type && el.type === 'showcase'
      })[0]
    },
    date: function () {
      let options = { day: 'numeric', month: 'long' }
      return (new Date(this.ownEvent.date)).toLocaleDateString('fr-FR', options)
    }
  }
}
</script>
