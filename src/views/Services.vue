<template>
  <div class="services">
    <Header :title="pages[page].Nom" :img="pages[page].Image[0].url"></Header>
    <!--<EventVignette :eventobj="item" v-for="item of ownEvents" :key="item.name"></EventVignette>-->
    <p class="page-desc">{{pages[page].Description}}</p>
    <EventTile v-for="event of ownEvents" :key="event.nom" :event="event"></EventTile>
    <div class="our-select">
      <div>
        <h3>Notre sélection</h3>
        <p>Retrouvez toutes les informations, les contenus et documents sélectionnés par nos soins à l’adresse placed.eu/#{{pages[page].Page}} ou en scannant le QR code.</p>
      </div>
      <div>
        <qrcode class="qrcode" :value="'https://placed.eu/#'+pages[page].Page" :options="{ width: 150 }"></qrcode>
      </div>
    </div>
    <div class="horizontal-scroller">
      <LinkVignette :linkobj="link" v-for="link of links" :key="link.Url"></LinkVignette>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import LinkVignette from '@/components/LinkVignette.vue'
import EventTile from '@/components/EventTile.vue'
import VueQrcode from '@chenfengyuan/vue-qrcode'

export default {
  name: 'patrimoine',
  components: {
    Header,
    EventTile,
    LinkVignette
  },
  props: [
    'page',
    'evenements',
    'pages',
    'links'
  ],
  methods: {
    relayPopup: function (label) {
      let ag = label
      //ag.event = this.ownEvent.name
      this.$emit('popup', ag)
    }
  },
  computed: {
    ownEvents: function () {
      return this.evenements.filter(el => {
        return el.Page === this.pages[this.page].Page
      })
    }
  }
}
</script>

<style scoped>
.page-desc {
  text-align: left;
  margin-left: 50px;
  font-size: 20px;
}

.our-select {
  width: calc(100% - 50px);
  float: left;
  text-align: left;
  margin-left: 50px;
  display: grid;
  grid-template-columns: 70% 1fr;
}

.qrcode {
  border-radius: 20px;
  margin-left: 50px;
}

.our-select h3 {
  font-size: 30px;
}

.our-select p {
  font-size: 20px;
}
</style>