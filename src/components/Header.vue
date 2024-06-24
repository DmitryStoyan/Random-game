<template>
  <header class="header">
    <a class="header__logo" href="#"> Random Game </a>
    <button
      class="header-menu__button"
      @click="isDownloadMenuModalOpen = true"
    ></button>
  </header>
  <DownloadMenu
    v-if="isDownloadMenuModalOpen"
    @close="isDownloadMenuModalOpen = false"
  />
</template>
<script>
import DownloadMenu from "./DownloadMenu.vue";
export default {
  components: {
    DownloadMenu,
  },

  emits: ["close"],

  data() {
    return {
      isDownloadMenuModalOpen: false,
    };
  },
  methods: {},
};
</script>
<style scoped>
.header {
  padding: 4rem 0 0 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header__logo {
  font-family: "DancingScript-Regular", serif;
  font-size: 2rem;
  font-weight: 900;
  color: aliceblue;
  text-decoration: none;
}

.header-menu__button {
  background: url(../images/random-icon_white.png);
  background-position: center;
  background-repeat: no-repeat;
  background-size: contain;
  width: 5.5rem;
  height: 5.5rem;
  border: none;
  cursor: pointer;
}

.popup_opened {
  opacity: 1;
  visibility: visible;
}
</style>
