<template>
  <div class="conferences">
    <Header :title="ownEvent.name" :img="ownEvent.image" :date="date" :icon="1"></Header>
    <h2>Autour de l'événement</h2>
    <ServiceVignette :eventobj="item" v-for="item of conferenceServices" :key="item.name"></ServiceVignette>
    <h2>Nos conférences filmées</h2>
    <div class="horizontal-scroller">
      <VideoVignette :videoobj="video" v-for="video of conferenceVideos" :key="video.name"></VideoVignette>
    </div>
    <div class="dual-container">
      <div class="half-width-container">
        <h2>Articles</h2>
        <ArticleVignette v-for="article of conferenceArticles" :key="article.name" :article="article"></ArticleVignette>
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
import VideoVignette from '@/components/VideoVignette.vue'
import ArticleVignette from '@/components/ArticleVignette.vue'
import ServiceVignette from '@/components/ServiceVignette.vue'

export default {
  name: 'conference',
  components: {
    Header,
    VideoVignette,
    ArticleVignette,
    ServiceVignette
  },
  props: [
    'events',
    'videos',
    'articles',
    'guichet',
    'services'
  ],
  methods: {
    relayPopup: function (label) {
      let ag = label
      ag.event = this.ownEvent.name
      this.$emit('popup', ag)
    }
  },
  computed: {
    ownEvent: function () {
      return this.events.filter((el) => {
        return el.type && el.type === 'conference'
      })[0]
    },
    conferenceVideos: function () {
      return this.videos.filter((el) => {
        return el.type && el.type === 'conference'
      })
    },
    conferenceArticles: function () {
      return this.articles.filter((el) => {
        return el.type && el.type === 'conference'
      })
    },
    conferenceServices: function () {
      return this.services.filter((el) => {
        return el.type && el.type === 'conference'
      })
    },
    date: function () {
      let options = { day: 'numeric', month: 'long' }
      return (new Date(this.ownEvent.date)).toLocaleDateString('fr-FR', options)
    }
  }
}
</script>
