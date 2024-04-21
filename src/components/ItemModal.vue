<template>
  <div @click="() => this.$emit('toggle-modal')" class="item-modal">
    <div class="item-modal-content" @click.stop="">
      <div class="item-name">
        <span id="item">{{ itemName }}</span>
      </div>
      <div id="sprite-container" class="sprite-container">
        <img :src="item.sprites.default" />
      </div>
      <div class="category">
        <span id="item">{{ catName }}</span>
      </div>
      <div class="description">
        <span v-for="(effect, index) in item.effect_entries" :key="index">{{
          effect.short_effect
        }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item"],
  data() {
    return {};
  },
  computed: {
    itemName() {
      return this.item.name
        .split("-")
        .map((el) => el[0].toUpperCase() + el.slice(1, el.length))
        .join(" ");
    },
    catName() {
      return this.item.category.name
        .split("-")
        .map((el) => el[0].toUpperCase() + el.slice(1, el.length))
        .join(" ");
    },
  },
};
</script>

<style scoped>
.item-modal {
  position: fixed;
  display: flex;
  justify-content: center;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
}

.item-modal-content {
  position: inherit;
  background-color: rgba(255, 255, 255, 0.4);
  color: var(--black);
  background-clip: padding-box;
  box-sizing: border-box;
  border-radius: 0.8rem;
  width: 20rem;
  top: 22.2rem;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: top;
  flex-direction: column;
  box-shadow: 0 0 0.625rem rgba(0, 0, 0, 0.3);
  padding: 0.8rem;
}

.sprite-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40%;
}

img {
  height: 4rem;
  margin: 0.5rem 0 0 0;
}

.description {
  text-align: center;
  text-justify: center;
  font-size: 0.8rem;
  color: var(--poke-yellow);
  text-shadow: 0.05rem 0.05rem 0.05rem var(--poke-blue);
  margin: 0 0.3rem 0.3rem 0.3rem;
}

.item-name {
  box-sizing: border-box;
  font-size: 2.2rem;
  color: var(--poke-yellow);
  -webkit-text-stroke: 0.1rem var(--poke-blue);
  text-shadow: -0.15rem 0.15rem 0.1rem var(--poke-blue-dark);
  font-family: "Helvetica Neue", sans-serif;
  font-weight: bold;
  text-align: center;
}

.category {
  box-sizing: border-box;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  letter-spacing: 0.08rem;
  text-transform: uppercase;
  color: var(--poke-yellow);
  font-weight: bold;
  text-shadow: -0.1rem 0.1rem 0.07rem var(--poke-blue-dark);
  font-family: "Helvetica Neue", sans-serif;
  text-align: center;
}

@media (max-device-width: 428px) {
  .help-modal-content {
    width: 25rem;
    height: 40rem;
  }
}
</style>
