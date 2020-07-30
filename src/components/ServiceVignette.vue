<template>
  <div class="service-vignette" @click="$parent.$emit('popup',{name:eventobj.name,url:eventobj.url,event:$parent.ownEvent.name})">
    <img  :src="eventobj.img"
          :style="{
            background: `linear-gradient(180deg, rgba(13, 12, 12, 0) 46.88%, #0D0C0C 100%), url(${eventobj.image})`,
            backgroundSize: 'cover'
          }"
    />
    <span class="service-vignette-name">{{eventobj.name}}</span>
  </div>
</template>

<script>
export default {
  props: [
    'eventobj'
  ]
}
</script>

<style scoped>
.service-vignette {
  width: 400px;
  margin-left: 75px;
  position: relative;
  flex-shrink: 0;
  display: inline-block;
}

.service-vignette-name {
  position: absolute;
  bottom: 6px;
  left: 50%;
  transform: translate(-50%,0);
  background-color: #0D0C0C;
  font-family: 'Jost';
  font-style: normal;
  font-weight: bold;
  font-size: 40px;
  line-height: 59px;
  text-align: center;
  width: fit-content;
  color: #FFFFFF;
}

img {
  border-radius: 20px;
  height: 300px;
  width: 100%;
}
</style>
