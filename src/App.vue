<template>
  <img id="logo" src="./assets/logo.png" />
  <div id="header">
    <p class="header">SEARCH APP</p>
  </div>
  <div class="main" id="main">
    <p class="input-caption">Search for Pokémon Name or ID:</p>
    <div class="inputs">
      <input
        @keyup.enter="search"
        v-model="searchInput"
        autocomplete="off"
        class="input-1"
        id="search-input"
        type="text"
        maxlength="20"
        title="Input name or ID"
        required
      />
      <button @click="search" class="button-1" id="search-button">
        Search
      </button>
      <span
        class="tooltip"
        data-text="ID must be between 1-1025 or 10001-10277. Click on sprite to play sound"
        ><i class="fa-solid fa-circle-info"></i
      ></span>
    </div>
  </div>
  <div v-if="pokemonNotFound" id="pokemon-container" class="pokemon-container">
    <div class="pokemon-container-inner">
      <div class="name-and-id">
        <span id="pokemon">Pokémon not found</span>
      </div>
    </div>
  </div>
  <pokemon-display v-else-if="pokemonFound" :pokemon="dat"></pokemon-display>
  <held-items v-if="hasItems" :items="itemsOnHand"></held-items>
  <stats-table v-if="pokemonFound" :stat="dat.stats"></stats-table>
</template>

<script>
import StatsTable from "./components/StatsTable.vue";
import PokemonDisplay from "./components/PokemonDisplay.vue";
import HeldItems from "./components/HeldItems.vue";

export default {
  name: "App",
  components: {
    StatsTable,
    PokemonDisplay,
    HeldItems,
  },
  data() {
    return {
      searchInput: "",
      stats: [],
      pokemonFound: false,
      pokemonNotFound: false,
      dat: {},
      spriteURL: {},
      hasItems: false,
      itemsOnHand: [],
    };
  },
  methods: {
    playSound() {
      if (this.dat.cries.latest) {
        const audio = new Audio(this.dat.cries.latest);
        audio.play();
      }
    },
    async search() {
      const input = this.searchInput.toLowerCase().trim().replace(" ", "-");
      if (!input) {
        this.pokemonNotFound = true;
        this.pokemonFound = false;
      } else {
        try {
          const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${input}`);
          this.dat = await res.json();
          if (this.dat.held_items[0]) {
            this.itemsOnHand.splice(0, this.itemsOnHand.length);
            this.hasItems = true;
            for (let i = 0; i < this.dat.held_items.length; i++) {
              fetch(`${this.dat.held_items[i].item.url}`)
                .then((res) => res.json())
                .then((dat) => {
                  this.itemsOnHand.push(dat);
                });
            }
          } else {
            this.hasItems = false;
          }
          this.pokemonFound = true;
          this.pokemonNotFound = false;
        } catch (err) {
          console.error(err);
          this.hasItems = false;
          this.pokemonNotFound = true;
          this.pokemonFound = false;
        }
      }
    },
  },
};
</script>

<style>
:root {
  --black: rgb(40, 40, 40);
  --poke-yellow: #ffcb05;
  --poke-yellow-dark: #c7a008;
  --poke-blue: #2a75bb;
  --poke-blue-dark: #3c5aa6;
  --background-transparent: rgba(255, 255, 255, 0.2);
}

#logo {
  margin-top: 0;
  width: 25rem;
}

.header {
  color: var(--poke-yellow);
  -webkit-text-stroke: 0.12rem var(--poke-blue);
  font-family: "Helvetica Neue", sans-serif;
  font-size: 2rem;
  font-weight: bold;
  line-height: 1;
  text-align: center;
  margin-top: -1rem;
  margin-bottom: 1rem;
}

.container {
  width: 25rem;
  min-height: 54rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: auto;
  margin-top: 1rem;
  margin-bottom: 1rem;
}

.main {
  background-color: var(--background-transparent);
  color: var(--black);
  border-radius: 0.3rem;
  width: 25rem;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  box-shadow: 0 0 0.625rem rgba(0, 0, 0, 0.3);
}

.input-caption {
  color: var(--poke-yellow);
  font-weight: bold;
  text-shadow: 0.15rem 0.15rem 0.15rem var(--poke-blue);
  text-align: center;
  font-size: 1rem;
  margin: 1rem;
  margin-bottom: 0;
}

.input-1 {
  align-items: center;
  background-color: var(--poke-yellow);
  border: 0.15rem solid var(--poke-blue);
  border-radius: 0.25rem;
  box-shadow: 0.07rem 0.15rem 0.625 #555;
  box-sizing: border-box;
  color: var(--poke-blue);
  display: inline-flex;
  font-family: system-ui, -apple-system, system-ui, "Helvetica Neue", Helvetica,
    Arial, sans-serif;
  font-size: 1rem;
  font-weight: 600;
  text-align: center;
  justify-content: center;
  line-height: 1.25;
  min-height: 1rem;
  height: 2rem;
  margin: 0;
}

.input-1:focus {
  border-color: var(--poke-blue-dark);
  outline: none;
}

.button-1 {
  align-items: center;
  background-color: var(--poke-yellow);
  border: 0.15rem solid var(--poke-blue);
  border-radius: 1rem;
  box-shadow: 0.07rem 0.15rem 0.625 #555;
  box-sizing: border-box;
  color: var(--poke-blue);
  cursor: pointer;
  display: inline-flex;
  font-family: system-ui, -apple-system, system-ui, "Helvetica Neue", Helvetica,
    Arial, sans-serif;
  font-size: 1rem;
  font-weight: 600;
  justify-content: center;
  line-height: 1.25;
  min-height: 1rem;
  height: 2rem;
  padding: calc(0.875rem - 0.07rem) calc(1.5rem - 0.07rem);
  position: relative;
  text-decoration: none;
  margin: 1rem;
  margin-right: 0;
  transition: all 250ms;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: baseline;
  width: auto;
}

.button-1:hover {
  border-color: var(--poke-blue-dark);
  color: var(--poke-blue-dark);
  transform: translate(0em, 0.15rem);
}

.tooltip {
  position: relative;
}

.tooltip i {
  margin-left: 1rem;
  color: var(--poke-yellow);
  animation-name: tilt;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  -webkit-filter: drop-shadow(0.07rem 0.15rem 0.15rem #222);
  filter: drop-shadow(0.07rem 0.15rem 0.15rem #222);
}

@keyframes tilt {
  50% {
    transform: rotate(25deg);
  }
}

.tooltip:before {
  content: attr(data-text);
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  left: 100%;
  margin-left: 0.94rem;
  width: 12.5rem;
  padding: 0.625;
  border-radius: 0.625;
  background: var(--poke-yellow);
  border: 0.23rem solid var(--poke-blue);
  color: var(--poke-blue);
  text-align: center;
  opacity: 0;
  transition: 0.5s opacity;
}

.tooltip:after {
  content: "";
  position: absolute;
  left: 100%;
  margin-left: -0.315rem;
  top: 50%;
  transform: translateY(-50%);
  border: 0.625 solid var(--poke-blue);
  border-color: transparent var(--poke-blue) transparent transparent;
  opacity: 0;
  transition: 0.5s opacity;
}
.tooltip:hover:before,
.tooltip:hover:after {
  opacity: 1;
}

@media (max-device-width: 768px) {
  .tooltip {
    display: none;
  }
}
@media (max-device-width: 480px) {
  .tooltip {
    display: none;
  }
}
</style>
