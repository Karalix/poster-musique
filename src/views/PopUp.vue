<template>
  <div class="popup-bg" @click="$emit('popup')">
    <div class="popup-box">
      <p>Envie de découvrir du contenu autour de {{label}} ?</p>
      <p>Rendez-vous ici : </p>
      <qrcode :value="url" :options="{ width: 200 }"></qrcode>
      <p>Rendez-vous sur la tablette, à l'événement "{{event}}"</p>
      <img src="/img/seetablet.svg"/>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueQrcode from '@chenfengyuan/vue-qrcode'

Vue.component(VueQrcode.name, VueQrcode)

export default {
  name: 'popup',
  props: ['label', 'url', 'event'],
  mounted: function () {
    setTimeout(() => {
      this.$emit('popup')
    }, 60000)
  }
}
</script>

<style scoped>
.popup-bg {
  position: fixed;
  width: 100vw;
  height: 100vh;
  background-color: rgba(70,70,70,0.5);
  backdrop-filter: blur(5px);
  z-index: 20;
}

.popup-box {
  margin-top: 50%;
  margin-left: 50%;
  transform: translate(-50%);
  border-radius: 20px;
  padding: 20px;
  text-align: center;
  background-color: black;
  width: 50%;
}

p {
  font-size: 35px;
}
</style>
