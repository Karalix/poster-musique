<template>
  <div class="template" @click="$parent.$emit('popup',{name:qa.q,url:qa.url,event:$parent.ownEvent.name})">
    <div class="question">
      {{qa.q}}
    </div>
    <div class="answer">
      {{qa.a}}
    </div>
  </div>
</template>

<script>
export default {
  props: ['qa']
}
</script>

<style scoped>

.question {
  margin-top: 30px;
  background-color: green;
  width: max-content;
  max-width: 60%;
  padding: 10px;
  border-radius: 10px;
  text-align: left;
}

.question::after {
  position: relative;
  display: inline-block;
  width: 10px;
  height: 20px;
  bottom: -25px;
  left: -20px;
  background-color: green;
  color: green;
  content: "  ";
  border-bottom-right-radius: 10px;
}

.answer {
  margin-top: 30px;
  background-color: darkcyan;
  width: max-content;
  max-width: 60%;
  padding: 10px;
  border-radius: 10px;
  margin-left: auto;
  text-align: left;
}

.answer::after {
  position: relative;
  display: block;
  width: 10px;
  height: 10px;
  bottom: -20px;
  right: -20px;
  background-color: darkcyan;
  color: darkcyan;
  content: "  ";
  border-bottom-left-radius: 10px;
}
</style>
