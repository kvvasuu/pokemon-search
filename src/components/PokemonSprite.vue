<template>
  <img @click="toggleShiny" id="sprite" :src="shiny" />
</template>

<script>
export default {
  props: ["sprite", "isShiny"],
  computed: {
    shiny() {
      if (this.sprite.front_shiny) {
        return this.isShiny
          ? this.sprite.front_shiny
          : this.sprite.front_default;
      } else return this.sprite.front_default;
    },
  },
  methods: {
    toggleShiny() {
      this.$emit("toggle-shiny");
    },
  },
};
</script>

<style>
#sprite {
  width: 100%;
  -webkit-filter: drop-shadow(0.625rem 0.625rem 0.625rem #222);
  filter: drop-shadow(0.625rem 0.625rem 0.625rem #222);
}

#sprite:active {
  transform: rotate(3deg);
}
</style>
