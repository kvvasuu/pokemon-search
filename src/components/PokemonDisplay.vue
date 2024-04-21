<template>
  <div id="pokemon-container" class="pokemon-container">
    <div class="pokemon-container-inner">
      <div class="name-and-id">
        <span id="pokemon"
          >{{ pokemon.name.toUpperCase() }} #{{ pokemon.id }}</span
        >
      </div>
      <div class="size">
        <span id="weight">Weight: {{ pokemon.weight }}</span>
        <span id="height"> Height: {{ pokemon.height }}</span>
      </div>
      <div id="sprite-container" class="sprite-container">
        <div class="image-caption">
          <span class="image-caption-text">Click me!</span>
        </div>
        <pokemon-sprite
          @toggle-shiny="() => this.$emit('toggle-shiny')"
          :sprite="pokemon.sprites"
          :isShiny="isShiny"
        ></pokemon-sprite>
      </div>
      <div id="types">
        <div
          v-for="typ in pokemon.types"
          class="type"
          :style="getIconColor(typ)"
          :key="typ.name"
        >
          <span>{{ typ.type.name }}</span>
          <span v-html="typeIcons[typ.type.name]"></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PokemonSprite from "./PokemonSprite.vue";

export default {
  props: ["pokemon", "isShiny"],
  components: {
    PokemonSprite,
  },
  data() {
    return {
      typeIcons: {
        normal: `<i class="fa-solid fa-user fa-lg"></i>`,
        fire: `<i class="fa-solid fa-fire fa-lg"></i>`,
        water: `<i class="fa-solid fa-water fa-lg"></i>`,
        electric: `<i class="fa-solid fa-bolt fa-lg"></i>`,
        grass: `<i class="fa-solid fa-leaf fa-lg"></i>`,
        ice: `<i class="fa-solid fa-snowflake fa-lg"></i>`,
        fighting: `<i class="fa-regular fa-sun fa-lg"></i>`,
        poison: `<i class="fa-solid fa-skull-crossbones fa-lg"></i>`,
        ground: `<i class="fa-solid fa-hill-rockslide fa-lg"></i>`,
        flying: `<i class="fa-solid fa-dove fa-lg"></i>`,
        psychic: `<i class="fa-solid fa-brain fa-lg"></i>`,
        bug: `<i class="fa-solid fa-bug fa-lg"></i>`,
        rock: `<i class="fa-solid fa-gem fa-lg"></i>`,
        ghost: `<i class="fa-solid fa-ghost fa-lg"></i>`,
        dragon: `<i class="fa-solid fa-dragon fa-lg"></i>`,
        dark: `<i class="fa-solid fa-moon fa-lg"></i>`,
        steel: `<i class="fa-solid fa-shield fa-lg"></i>`,
        fairy: `<i class="fa-solid fa-wand-magic-sparkles fa-lg"></i>`,
      },
    };
  },
  methods: {
    getIconColor(type) {
      return { color: `var(--${type.type.name})` };
    },
    playSound() {
      if (this.pokemon.cries.latest) {
        const audio = new Audio(this.pokemon.cries.latest);
        audio.volume = 0.1;
        audio.play();
      }
    },
  },
};
</script>

<style>
:root {
  /* Types colors declaration*/
  --normal: #b7b7aa;
  --fire: #ff5837;
  --water: #42a1ff;
  --electric: #fecc33;
  --grass: #78cc55;
  --ice: #66ccfe;
  --fighting: #d3887e;
  --poison: #b8008a;
  --ground: #dfba52;
  --flying: #8899ff;
  --psychic: #ff66a3;
  --bug: #aabb23;
  --rock: #baaa66;
  --ghost: #9995d0;
  --dragon: #9e93f1;
  --dark: #b59682;
  --steel: #abaabb;
  --fairy: #ed99ed;
}

.pokemon-container {
  background-color: var(--background-transparent);
  color: var(--black);
  border-radius: 0.3rem;
  width: 25rem;
  height: 22.5rem;
  margin: 1rem 0 0 0;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  box-shadow: 0 0 0.625rem rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(5px);
}

.pokemon-container-inner {
  background-color: rgba(255, 255, 255, 0.3);
  color: var(--black);
  border-radius: 0.2rem;
  width: 96%;
  height: 96%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.name-and-id {
  box-sizing: border-box;
  font-size: 2rem;
  color: var(--poke-yellow);
  -webkit-text-stroke: 0.07rem var(--poke-blue);
  text-shadow: 0.15rem 0.15rem 0.15rem var(--poke-blue);
  font-family: "Helvetica Neue", sans-serif;
  font-weight: bold;
  text-align: center;
}

.size {
  font-size: 1.2rem;
  text-shadow: 0.15rem 0.15rem 0.15rem var(--poke-blue);
  color: var(--poke-yellow);
}

.sprite-container {
  width: 40%;
}

.image-caption {
  position: relative;
}

.image-caption-text {
  display: block;
  top: 1.2rem;
  position: absolute;
  transform: rotate(-40deg);
  color: var(--poke-yellow);
  font-weight: bold;
  text-shadow: 0.1rem 0.1rem 0.1rem var(--poke-blue);
  text-align: center;
  font-size: 0.6rem;
  z-index: 1;
  -webkit-text-stroke: 0.03rem rgba(0, 0, 0, 0.3);
}

#types {
  min-height: 3.125rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.315rem;
}

.type {
  letter-spacing: 1px;
  height: 3.125rem;
  width: 5rem;
  padding: 0.7rem;
  font-size: 1rem;
  text-align: center;
  border-radius: 0.625rem;
  text-transform: uppercase;
  font-weight: bold;
  text-shadow: 0.07rem 0.07rem 0.23rem #222;
  -webkit-text-stroke: 0.07rem rgba(0, 0, 0, 0.3);
}

.type i {
  margin: 1rem;
}
</style>
