<template>
  <div class="menu" tabindex="-1" @keydown.esc="close">
    <div class="menu__content">
      <div class="install-screen">
        <button class="menu__close-button" @click="close"></button>
        <img
          class="icon"
          src="<%=require('./images/random-icon.png')%>"
          alt=""
        />

        <p class="subtitle">Random Game</p>
        <div class="wrapper">
          <button class="download-button">Скачать игру на телефон</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  emits: ["close"],

  methods: {
    close() {
      this.$emit("close");
    },
  },

  mounted() {
    this.$el.focus();
  },
};
</script>
<style scoped>
.menu {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 5;
  background: wheat;
  /* visibility: hidden;
  opacity: 0; */
  transition: opacity 0.5s ease;
}

.menu__close-button {
  position: absolute;
  top: 3rem;
  right: 3rem;
  background: url(../images/close.svg);
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  width: 32px;
  height: 32px;
  border: none;
  cursor: pointer;
}

.icon {
  display: block;
  width: 30rem;
  margin: auto;
  margin-top: 20rem;
}

.subtitle {
  font-size: x-large;
  margin-top: 7rem;
  width: 100%;
  text-align: center;
  color: black;
}
.wrapper {
  width: 100%;
  text-align: center;
}
.download-button {
  margin: 7rem 0 0;
  padding: 1rem 2rem;
  background-color: black;
  color: aliceblue;
  font-size: 2.1rem;
}
</style>
