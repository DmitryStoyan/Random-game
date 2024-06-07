<template>
  <div class="app">
    <div class="page">
      <Header />
      <DownloadMenu />
    </div>
  </div>
</template>
<script>
import Header from "./components/Header.vue";
import DownloadMenu from "./components/DownloadMenu.vue";

export default {
  components: {
    Header,
    DownloadMenu,
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
  height: 100vh;
  margin: 0 auto;
  max-width: 90%;
  width: 120rem;
}
</style>
