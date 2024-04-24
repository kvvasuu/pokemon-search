<template>
  <img id="logo" src="./assets/logo.png" />
  <div id="header">
    <p class="header">SEARCH APP</p>
  </div>
  <div class="main" id="main">
    <div class="main-header">
      <p class="input-caption">Search for Pokémon Name or ID:</p>
      <i
        v-if="mute"
        @click="toggleMute"
        class="fa-solid fa-volume-xmark mute-button"
      ></i>
      <i
        v-else
        @click="toggleMute"
        class="fa-solid fa-volume-high mute-button"
      ></i>
    </div>

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
      <span @click="helpModalHandle" class="help-button"
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
  <pokemon-display
    v-else-if="pokemonFound"
    :pokemon="dat"
    :isShiny="isShiny"
    @toggle-shiny="playSound(), toggleShiny()"
  ></pokemon-display>
  <held-items v-if="hasItems" :items="itemsOnHand"></held-items>
  <stats-table v-if="pokemonFound" :stat="dat.stats"></stats-table>
  <transition name="fade" appear>
    <help-modal
      v-if="helpModalShow"
      @toggle-modal="helpModalHandle"
      :mute="mute"
    ></help-modal>
  </transition>
</template>

<script>
const kwasu = {
  height: 184,
  weight: 93,
  held_items: [
    {
      item: {
        name: "metal-powder",
        url: "https://pokeapi.co/api/v2/item/234/",
      },
    },
    {
      item: {
        name: "quick-powder",
        url: "https://pokeapi.co/api/v2/item/251/",
      },
    },
  ],
  cries: {
    latest:
      "https://raw.githubusercontent.com/PokeAPI/cries/main/cries/pokemon/latest/45.ogg",
  },
  id: 0,
  name: "Kwasu",
  sprites: {
    front_default:
      "https://raw.githubusercontent.com/kvvasuu/pokemon-search/master/src/assets/kvvasu.png",
  },
  stats: [
    {
      base_stat: 99,
      effort: 1,
      stat: {
        name: "hp",
        url: "https://pokeapi.co/api/v2/stat/1/",
      },
    },
    {
      base_stat: 99,
      effort: 0,
      stat: {
        name: "attack",
        url: "https://pokeapi.co/api/v2/stat/2/",
      },
    },
    {
      base_stat: 99,
      effort: 0,
      stat: {
        name: "defense",
        url: "https://pokeapi.co/api/v2/stat/3/",
      },
    },
    {
      base_stat: 99,
      effort: 0,
      stat: {
        name: "special-attack",
        url: "https://pokeapi.co/api/v2/stat/4/",
      },
    },
    {
      base_stat: 99,
      effort: 0,
      stat: {
        name: "special-defense",
        url: "https://pokeapi.co/api/v2/stat/5/",
      },
    },
    {
      base_stat: 99,
      effort: 0,
      stat: {
        name: "speed",
        url: "https://pokeapi.co/api/v2/stat/6/",
      },
    },
  ],
  types: [
    {
      slot: 1,
      type: {
        name: "normal",
        url: "https://pokeapi.co/api/v2/type/1/",
      },
    },
  ],
};

import StatsTable from "./components/StatsTable.vue";
import PokemonDisplay from "./components/PokemonDisplay.vue";
import HeldItems from "./components/HeldItems.vue";
import HelpModal from "./components/HelpModal.vue";

export default {
  name: "App",
  components: {
    StatsTable,
    PokemonDisplay,
    HeldItems,
    HelpModal,
  },
  data() {
    return {
      helpModalShow: false,
      mute: false,
      isShiny: false,
      searchInput: "",
      currentSearch: "",
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
    helpModalHandle() {
      this.helpModalShow = !this.helpModalShow;
    },
    toggleMute() {
      this.mute = !this.mute;
    },
    toggleShiny() {
      this.isShiny = !this.isShiny;
    },
    playSound() {
      if (this.dat.cries.latest && !this.mute) {
        const audio = new Audio(this.dat.cries.latest);
        audio.volume = 0.1;
        audio.play();
      }
    },
    async search() {
      const input = this.searchInput.toLowerCase().trim().replace(" ", "-");
      if (!input) {
        this.pokemonNotFound = true;
        this.pokemonFound = false;
      } else if (this.currentSearch !== this.searchInput) {
        try {
          if (input === "kvvasu" || input === "kwasu" || input === "0") {
            this.dat = kwasu;
          } else {
            const res = await fetch(
              `https://pokeapi.co/api/v2/pokemon/${input}`
            );
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
          }
          this.isShiny = false;
          this.pokemonFound = true;
          this.pokemonNotFound = false;
          this.playSound();
          this.currentSearch = this.searchInput;
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
  -webkit-text-stroke: 0.12rem rgba(42, 117, 187, 1);
  text-shadow: -0.15rem 0.15rem 0.07rem var(--poke-blue-dark);
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
  align-items: center;
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
  backdrop-filter: blur(5px);
}

.main-header {
  width: 25rem;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.mute-button {
  position: relative;
  top: 0.4rem;
  left: 1.6rem;
  font-size: 1rem;
  color: var(--poke-yellow);
  -webkit-filter: drop-shadow(0.07rem 0.15rem 0.15rem #222);
  filter: drop-shadow(0.07rem 0.15rem 0.15rem #222);
  cursor: pointer;
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

.help-button {
  position: relative;
  cursor: help;
}

.help-button i {
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
  animation: blur-in 0.5s ease-in-out forwards;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  animation: blur-out 0.5s ease-in-out forwards;
}
</style>
