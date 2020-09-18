<template>
  <div id="app">
    <PopUp :label="popuplabel" :url="popupurl" :event="popupevent" v-if="showPopup" @popup="closePopup"></PopUp>
    <Services :evenements="evenements" :pages="pages" :page="slidesPos" :links="links" @popup="togglePopup"></Services>
    <div v-if="showNightScreen" id="night-screen"></div>
  </div>
</template>


<script>
import Airtable from 'airtable'
import Services from './views/Services'
import PopUp from './views/PopUp'

export default {
  data: function () {
    return {
      evenements: [],
      pages: [],
      links: [],
      showShowcase: true,
      showVideo: false,
      slidesPos: 0,
      nbSlides: 3,
      showPopup: false,
      popuplabel: 'ceci',
      popupurl: 'https://bm-lyon.fr',
      showNightScreen: false
    }
  },
  components: {
    Services,
    PopUp
  },
  methods: {
    togglePopup: function (label) {
      this.popuplabel = label.name
      this.popupurl = label.url
      this.popupevent = label.event
      this.showPopup = true
    },
    closePopup: function () {
      this.showPopup = false
    }
  },
  mounted: function () {
    let self = this
    /*setInterval(() => {
      if (this.slidesPos === this.nbSlides - 1) {
        this.slidesPos = 0
      } else {
        this.slidesPos += 1
      }
    }, 20000)*/

    setInterval(() => {
      let currentTime = new Date()
      if (currentTime.getDay() < 1 || currentTime.getHours() >= 21 || currentTime.getHours() < 8) {
        this.showNightScreen = true
      } else {
        this.showNightScreen = false
      }
    }, 60000)

    Airtable.configure({
      endpointUrl: 'https://api.airtable.com',
      apiKey: 'keyHLqvz6NRbhxNy4'
    })
    var base = Airtable.base('appzie6SWUMPaqojZ')

    base('evenement').select({
      // Selecting the first 3 records in Grid view:
      maxRecords: 20,
      view: 'Grid view'
    }).eachPage(function page (records, fetchNextPage) {
      records.forEach(function (record) {
        // console.log(record.fields);
        self.evenements.push(record.fields)
      })
      fetchNextPage()
    }, function done (err) {
      if (err) { console.error(err) }
    })
    
    base('page').select({
      // Selecting the first 3 records in Grid view:
      maxRecords: 20,
      view: 'Grid view'
    }).eachPage(function page (records, fetchNextPage) {
      records.forEach(function (record) {
        // console.log(record.fields);
        self.pages.push(record.fields)
      })
      fetchNextPage()
    }, function done (err) {
      if (err) { console.error(err) }
    })
    
    base('lien').select({
      // Selecting the first 3 records in Grid view:
      maxRecords: 20,
      view: 'Grid view'
    }).eachPage(function page (records, fetchNextPage) {
      records.forEach(function (record) {
        // console.log(record.fields);
        self.links.push(record.fields)
      })
      fetchNextPage()
    }, function done (err) {
      if (err) { console.error(err) }
    })
  }
}
</script>

<style>
#app {
  font-family: 'Jost', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}

body {
  margin: 0;
  background-color: #0D0C0C;
  scrollbar-width: none;
}

body::-webkit-scrollbar {
  display: none;
}

.horizontal-scroller {
  overflow-x: scroll;
  overflow-y: hidden;
  display: flex;
  flex-flow: row;
  flex-wrap: nowrap;
  scrollbar-width: none; /* For Firefox */
  width: 100%;
  margin-top: 22px;
}

.horizontal-scroller::-webkit-scrollbar {
 width: 0px;
}

h2 {
  font-family: 'Jost';
  font-style: normal;
  font-weight: bold;
  font-size: 60px;
  line-height: 89px;
  /* identical to box height */
  font-feature-settings: 'ss01' on;
  color: #FFFFFF;
  margin-left: 75px;
  margin-bottom: 10px;
  margin-top: 10px;
  text-align: left;
}

.slide-enter-active {
  transition: all 1s;
}

.slide-leave-active {
  transition: all 0s;
}

.slide-enter, .slide-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateX(20px);
}

.dual-container {
  display: flex;
}

.half-width-container {
  width: 440px;
  margin-left: 75px;
}

.half-width-container > * {
  margin-left: 0;
}

.rdv-tablet {
  font-size: 30px;
  text-align: right;
  margin-right: 75px;
}

#night-screen {
  width: 100vw;
  height: 100vh;
  position: fixed;
  background-color: black;
  top: 0;
}
</style>
