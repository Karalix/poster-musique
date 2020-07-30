<template>
  <div class="article-vignette-container" @click="$parent.$emit('popup',{name:article.name,url:article.url,event:$parent.ownEvent.name})">
    <img :src="article.image" class="article-img">
    <div class="article-title">{{article.name}}</div>
  </div>
</template>

<script>
export default {
  props: ['article']
}
</script>

<style scoped>
.article-img {
  width: 145px;
  height: 145px;
  object-fit: cover;
  display: inline-block;
}

.article-vignette-container {
  text-align: left;
  width: 466px;
  vertical-align: top;
  margin-top: 6px;
}

.article-title {
  font-size: 30px;
  display: inline-block;
  max-width: 304px;
  margin-left: 16px;
  vertical-align: top;
}
</style>

