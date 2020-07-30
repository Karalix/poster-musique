<template>
  <div class="video-vignette" @click="$parent.$emit('popup',{name:videoobj.name,url:videoobj.url,event:$parent.ownEvent.name})">
    <img  class="video-vignette-img"
          :style="{
            background: `linear-gradient(180deg, rgba(13, 12, 12, 0) 46.88%, #0D0C0C 100%), url(${videoobj.image})`,
            backgroundSize: 'cover'
          }"
    />
    <img class="play-icon" src="/img/play.svg"/>
    <span class="video-vignette-name">{{videoobj.name}}</span>
  </div>
</template>

<script>
export default {
  props: [
    'videoobj'
  ]
}
</script>

<style scoped>
.video-vignette {
  width: 400px;
  margin-left: 75px;
  position: relative;
  flex-shrink: 0;
}

.video-vignette-name {
  position: absolute;
  bottom: 8px;
  left: 50%;
  transform: translate(-50%,0);
  background-color: #0D0C0C;
  font-family: 'Jost';
  font-style: normal;
  font-weight: bold;
  font-size: 20px;
  line-height: 59px;
  text-align: center;
  width: fit-content;
  color: #FFFFFF;
}

.video-vignette-img {
  border-radius: 20px;
  height: 267px;
  width: 100%;
}

.play-icon {
  position: absolute;
  top: 10px;
  width: 69px;
  left: 63px;
  transform: translate(-50%,25%);
}
</style>
