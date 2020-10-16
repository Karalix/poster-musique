<template>
  <div class="services">
    
    <div class="progress-bar">
      <div class="progress-segment" :class="{past: isPastPage(index), current: isCurrentPage(index)}" v-for="(pagx, index) of pages" :key="index">
      </div>
    </div>
    <Header :title="pages[page].Nom" :img="pages[page].Image[0].url"></Header>
    <!--<EventVignette :eventobj="item" v-for="item of ownEvents" :key="item.name"></EventVignette>-->
    <p class="page-desc" v-html="htmlDescription"></p>
    <div id="main-content-wrapper">
    <EventTile v-for="event of ownEvents" :key="event.nom" :event="event"></EventTile>
    <DescriptionTile :event="event" :key="event.Nom" v-for="event of ownDesc"></DescriptionTile>
    </div>
    <div class="our-select">
      <div>
        <h3>Notre sélection</h3>
        <p>Retrouvez toutes les informations, les contenus et documents sélectionnés par nos soins à l’adresse <em class="underline">placed.eu/#{{pages[page].Page}}</em> ou en scannant le QR code.</p>
      </div>
      <div>
        <qrcode class="qrcode" :value="'https://placed.eu/#'+pages[page].Page" :options="{ width: 150 }"></qrcode>
      </div>
    </div>
    <div class="horizontal-scroller">
      <LinkVignette :linkobj="link" v-for="link of ownLinks" :key="link.Url"></LinkVignette>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import LinkVignette from '@/components/LinkVignette.vue'
import EventTile from '@/components/EventTile.vue'
import VueQrcode from '@chenfengyuan/vue-qrcode'
import DescriptionTile from '@/components/DescriptionTile.vue'

export default {
  name: 'services',
  components: {
    Header,
    EventTile,
    LinkVignette,
    DescriptionTile
  },
  props: [
    'page',
    'evenements',
    'pages',
    'links',
    'desc'
  ],
  methods: {
    relayPopup: function (label) {
      let ag = label
      //ag.event = this.ownEvent.name
      this.$emit('popup', ag)
    },
    isPastPage: function (index) {
      return index < this.page
    },
    isCurrentPage: function (index) {
      return index === this.page
    }
  },
  computed: {
    ownEvents: function () {
      return this.evenements.filter(el => {
        return el.Page === this.pages[this.page].Page
      })
    },
    ownDesc: function () {
      return this.desc.filter(el => {
        return el.Page === this.pages[this.page].Page
      })
    },
    ownLinks: function () {
      return this.links.filter(el => {
        return el.Page === this.pages[this.page].Page
      })
    },
    htmlDescription: function () {
      return this.pages[this.page].Description.replaceAll(/\n/g, '<br/>')
    }
  }
}
</script>

<style scoped>
.page-desc {
  text-align: left;
  margin-left: 50px;
  margin-right: 50px;
  font-size: 20px;
}

.our-select {
  width: calc(100% - 50px);
  float: left;
  text-align: left;
  margin-left: 50px;
  margin-top: 50px;
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

#main-content-wrapper {
  min-height: 450px;
}

.underline {
  text-decoration: underline;
}

.progress-bar {

  position: fixed;
  top : 0;
  width: 100%;
  display: flex;
  flex-direction: row;
}

.progress-segment {
  flex: 1 0 auto;
  height: 10px;
  border-radius: 10px;
  background-color: #181818;
  margin: 20px;
}

.past {
  background-color: white;
}

.current {
  background-color: white;
  animation: blinker 1s linear infinite;
}

@keyframes blinker {
  50% {
    background-color: #181818;
  }
}
</style>