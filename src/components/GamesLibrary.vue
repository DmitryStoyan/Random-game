<template>
  <div class="game-library">
    <article
      v-for="(game, index) in games"
      :key="index"
      class="game-library__item"
      @click="toggleSelection(game.name)"
    >
      <img class="game-library__img" :src="game.imgLibrary" :alt="game.name" />
      <div
        class="overlay"
        :class="{ overlay_active: selectedGames.includes(game.name) }"
      >
        <img
          class="overlay-logo"
          src="../images/random-icon_white.png"
          alt="Logo"
        />
      </div>
    </article>
  </div>
</template>

<script>
export default {
  props: {
    games: {
      type: Array,
      required: true,
    },
    selectedGames: {
      type: Array,
      required: true,
    },
  },
  methods: {
    toggleSelection(gameName) {
      this.$emit("toggle-game-selection", gameName);
    },
  },
};
</script>

<style scoped>
.game-library {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  width: 100%;
  justify-content: center;
  margin: 3rem 0 0 0;
}

.game-library__item {
  position: relative;
  cursor: pointer;
}

.game-library__img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease;
}

.overlay-logo {
  width: 50px;
  height: 50px;
}

.overlay_active {
  opacity: 1;
  visibility: visible;
}

@media (max-width: 1024px) {
  .game-library {
    display: grid;
    grid-template-columns: repeat(3, minmax(100px, 1fr));
    gap: 1.4rem;
    width: 100%;
    justify-content: center;
    list-style-type: none;
  }

  @media (max-width: 768px) {
    .game-library {
      gap: 1rem;
    }
  }

  @media (max-width: 375px) {
    .game-library {
      grid-template-columns: repeat(1, 1fr);
      gap: 2rem;
      width: 100%;
      justify-content: center;
    }
  }
}
</style>
