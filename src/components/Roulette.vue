<template>
  <div class="roulette">
    <div class="pointer"></div>
    <div class="app">
      <div class="scope">
        <ul class="list"></ul>
      </div>
      <my-button class="btn" @click="start">Крутить</my-button>
    </div>
  </div>
</template>

<script>
import { initialRouletteImg } from "../initialRouletteImg";
import { initialGames } from "../initialGames";
import MyButton from "./UI/MyButton.vue";

export default {
  components: {
    MyButton,
  },
  data() {
    return {
      name: "secret",
      img: initialRouletteImg.secret,
      cells: 243,
      selectedGames: initialGames,
      observer: null,
      isStarted: false,
    };
  },
  mounted() {
    this.generateItems();
  },
  methods: {
    getItem() {
      if (this.selectedGames.length === 0) {
        return { name: "secret", img: initialRouletteImg.secret };
      }

      const randomIndex = Math.floor(Math.random() * this.selectedGames.length);
      const selectedGameName = this.selectedGames[randomIndex].name
        .toLowerCase()
        .replace(/\s+(\d)/g, "$1");
      return {
        name: this.selectedGames[randomIndex].name,
        img: initialRouletteImg[selectedGameName],
      };
    },
    generateItems() {
      const listElement = document.querySelector(".list");
      if (listElement) {
        listElement.innerHTML = "";
      }
      const scopeElement = document.querySelector(".scope");
      if (scopeElement) {
        scopeElement.innerHTML = "<ul class='list'></ul>";
      }
      const list = document.querySelector(".list");

      this.observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              // chopSound.pause();
              // chopSound.currentTime = 0;
              // chopSound.play();
            }
          });
        },
        {
          root: document.querySelector(".scope"),
          threshold: 0.9,
        }
      );

      for (let i = 0; i < this.cells; i++) {
        const item = this.getItem();
        const li = document.createElement("li");

        li.setAttribute("data-item", JSON.stringify(item));
        li.classList.add("list__item");
        li.innerHTML = `<img class='list__item-image' src='${item.img}' alt='${item.name}'>`;

        list.append(li);

        this.observer.observe(li);
      }
    },
    start() {
      if (this.isStarted) {
        return;
      } else {
        this.isStarted = true;
      }

      this.generateItems();

      // const list = document.querySelector(".list");
      const list = this.$el.querySelector(".list");

      setTimeout(() => {
        list.style.left = "50%";
        list.style.transform = "translate3d(-50%, 0, 0)";
      }, 0);

      list.addEventListener("transitionend", () => {
        this.isStarted = false;
        this.observer.disconnect();
        const items = list.querySelectorAll(".list__item");
        const centerItemIndex = Math.floor(items.length / 2);
        const centerItem = items[centerItemIndex];

        if (centerItem) {
          // winSound.play();
          const data = JSON.parse(centerItem.getAttribute("data-item"));
          console.log("Итоговый элемент:", data);
          centerItem.classList.add("active");
        }
      });
    },
  },
};
</script>

<style>
.roulette {
  position: relative;
  margin: 25rem 0 0 0;
}

.active {
  opacity: 1 !important;
}

.pointer {
  background-image: url(@/images/pointer-theme-dark.png);
  background-position: center;
  background-size: cover;
  position: absolute;
  left: 50%;
  top: 0.5rem;
  transform: translate3d(-50%, -25px, 0);
  height: 4rem;
  width: 4rem;
  z-index: 2;
}

.pointer-theme-dark {
  background-image: url(@/images/pointer-theme-dark.png);
}

.pointer-theme-light {
  background-image: url(@/images/pointer.png);
}

.app {
  position: relative;
  margin: 0 auto;
  background: #1b1f24;
  border-radius: 10px;
  overflow: hidden;
}

.scope {
  overflow: hidden;
}

.list {
  position: relative;
  display: inline-flex;
  left: 0;
  min-height: 150px;
  transform: translate3d(0, 0, 0);
  list-style: none;
  transition: 15s cubic-bezier(0.21, 0.53, 0.29, 0.99);
}

.list__item {
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 20rem;
  opacity: 0.5;
  transition: 0.3s ease;
}

.list__item:nth-child(2n) {
  background: rgba(0, 0, 0, 0.1);
}

.list__item-image {
  width: 80%;
  height: 80%;
  object-fit: contain;
  transition: 0.3s ease;
}

@media (max-width: 1024px) {
  .roulette {
    margin: 30rem 0 0 0;
  }
}

@media (max-width: 768px) {
  .roulette {
    margin: 20rem 0 0 0;
  }
}

@media (max-width: 500px) {
  .roulette {
    margin: 30rem 0 0 0;
  }
}

@media screen and (max-width: 480px) {
  .app {
    position: relative;
    background: #1b1f24;
    border-radius: 10px;
  }
}
</style>
