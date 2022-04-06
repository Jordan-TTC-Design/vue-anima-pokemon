<script setup>
import { computed, onMounted, ref } from 'vue';
const progress = ref(0);
const fixClass = computed(() => {
  return progress.value < 1;
});
onMounted(() => {
  const section2Width = document.querySelector('#section2');
  const app = document.querySelector('#app');
  app.addEventListener('scroll', () => {
    if (app.scrollTop < window.innerHeight) {
      progress.value = 0;
      section2Width.scrollTo({
        left: 0,
      });
    } else if (app.scrollTop > window.innerHeight * 4) {
      progress.value = 1;
    } else {
      progress.value =
        (app.scrollTop - window.innerHeight) / (window.innerHeight * 3);
      let position =
        (section2Width.scrollWidth - window.innerWidth) * progress.value;
      section2Width.scrollTo({ left: position });
    }
  });
});
</script>

<template>
  <!-- 需要高度撐出捲軸高度 -->
  <div class="section section--text">
    <h2>出發吧～前往洗翠地區！</h2>
  </div>
  <div
    id="section2"
    class="section section--flex"
    :class="{ 'section--sticky': fixClass }"
  >
    <div class="section bgR" :class="{ 'section--static': fixClass }"></div>
    <div class="section bgG" :class="{ 'section--static': fixClass }"></div>
    <div class="section bgB" :class="{ 'section--static': fixClass }"></div>
    <div class="section bgB" :class="{ 'section--static': fixClass }"></div>
  </div>
  <div class="section bgG" :class="{ 'section--static': fixClass }"></div>
  <div class="section bgB" :class="{ 'section--static': fixClass }"></div>
  <div class="section bgB" :class="{ 'section--static': fixClass }"></div>
  <div class="section section--text">
    <h2>出發吧～前往洗翠地區！</h2>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  overflow: hidden;
}
#app {
  width: 100vw;
  height: 100vh;
  overflow: auto;
}
.section {
  position: relative;
  width: 100%;
  height: 100%;
  background-color: #fff;
  overflow: hidden;
}
.section--text {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 64px;
}
#section2,
#section3 {
  background-color: #e2e2e2;
}
#section2 {
  --scale: 3;
  -ms-overflow-style: none;
  overflow: -moz-hidden-unscrollable;
  overflow: hidden;
}
#section2::-webkit-scrollbar {
  display: none;
}
.section--flex {
  display: flex;
  flex-wrap: nowrap;
}
.section--flex .section {
  width: 100vw;
  min-width: 100vw;
}

#section3 {
  --scale: 1;
}
.section--sticky {
  position: sticky;
  top: 0;
  left: 0;
}
.section--static {
  position: static;
}
.bgR {
  background: red;
}
.bgG {
  background: green;
}
.bgB {
  background: blue;
}
</style>
