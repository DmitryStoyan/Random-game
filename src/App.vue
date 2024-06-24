<template>
  <div class="app">
    <div class="page">
      <Header />
      <Roulette />
    </div>
  </div>
</template>
<script>
import Header from "./components/Header.vue";
import Roulette from "./components/Roulette.vue";

export default {
  components: {
    Header,
    Roulette,
  },
  methods: {},
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}
.app {
  background: #13161a;
  color: white;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  transition: background 0.6s ease;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.page {
  display: flex;
  flex-direction: column;
  /* height: 100vh; */
  margin: 0 auto;
  max-width: 90%;
  width: 120rem;
}

@media (max-width: 1024px) {
  html {
    font-size: calc(100vw / 768 * 10);
  }
}

@media (max-width: 768px) {
  html {
    font-size: calc(100vw / 500 * 10);
  }

  .page {
    max-width: 95%;
  }
}

@media (max-width: 500px) {
  html {
    font-size: calc(100vw / 500 * 10);
  }
}

@media screen and (max-width: 480px) {
  .app {
    position: relative;
    background: #1b1f24;
    border-radius: 10px;
  }
}

@media (max-width: 375px) {
  html {
    font-size: calc(100vw / 375 * 10);
  }
}
</style>
