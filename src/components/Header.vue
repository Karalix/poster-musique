<template>
  <div class="poster-header"
      :style="{
            background: `linear-gradient(180deg, rgba(13, 12, 12, 0) 52.08%, #0D0C0C 100%), linear-gradient(180deg, #000000 0%, rgba(0, 0, 0, 0) 50.52%), url(${img})`,
            backgroundSize: 'cover',
            backgroundRepeat: 'no-repeat',
            backgroundPositionY: '50%'
        }">
    <div class="header-box">
      <div class="header-right">
        <h1>{{title}}</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'title',
    'img',
    'date',
    'icon'
  ],
  methods: {
    getIcon: function (index) {
      switch (index) {
        case 0:
          return '/img/vox-player.gif'
        case 1:
          return '/img/live-video-on.gif'
        case 2:
          return '/img/sound.gif'
        default:
          return '/img/sound.gif'
      }
    }
  }
}
</script>

<style scoped>
.poster-header {
  width: 100%;
  height: 500px;
}

.header-box {
  position: absolute;
  top: 200px;
  margin-top: 100px;
  margin-left: 50px;
  margin-right: 50px;
  /*margin-bottom: 10px;*/
  text-align: left;
}

.header-box img {
  margin-top: 50%;
  padding: 20px;
  border-radius: 50px;
  background-color: white;
}

h1 {
  text-transform: none;
  font-family: 'Jost';
  font-style: normal;
  font-weight: bold;
  font-size: 64px;
  line-height: 1.6em;
  /* identical to box height */
  font-feature-settings: 'ss01' on;
  color: #FFFFFF;
  margin:5px;
}

h2 {
  margin: 5px;
  font-size: 40px;
}
</style>
