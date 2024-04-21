<template>
  <div @click="() => this.$emit('toggle-modal')" class="help-modal">
    <div class="help-modal-content" @click.stop="">
      <div class="help-modal-header">
        <p>HELP</p>
      </div>
      <ul>
        <li>
          <p class="instructions-header">How to use it?</p>
          <p class="instructions">
            Enter the Pokémon's name or ID. The ID must be in the range 1-1025
            or 10001-10277. After pressing the "search" button, if a suitable
            Pokemon is found, it will be displayed.
          </p>
          <hr />
          <p class="instructions">
            By pressing on a Pokémon you can change its appearance to "Shiny"
            and play its sound.<br />You can mute sounds by pressing the speaker
            icon in the upper right corner, above the "info" icon.
          </p>
          <hr />
          <p class="instructions">
            If the Pokémon has any items, they will be displayed.<br />By
            clicking on an item you can check its details.
          </p>
          <hr />
          <p class="instructions">
            A table with statistics is displayed below.
          </p>
          <hr />
          <p class="instructions">
            The information is mostly based on video game franchise.<br />
            Data is obtained from
            <a href="https://pokeapi.co/" target="_blank">PokeAPI</a>
          </p>
        </li>
        <div class="copyright-container"></div>
      </ul>
      <p class="copyright">
        &copy; Copyright 2024. All rights reserved. Powered by
        <a href="https://github.com/kvvasuu" target="_blank">Kvvasu</a>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["mute"],
};
</script>

<style scoped>
.help-modal {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(2px);
}

.help-modal-content {
  background-color: var(--poke-yellow);
  border: 0.5rem solid var(--poke-blue);
  box-sizing: border-box;
  color: var(--poke-blue);
  border-radius: 0.8rem;
  width: 35rem;
  min-height: 32.5rem;
  margin: 1rem 0 0 0;
  padding: 0 1rem 0 1rem;
  display: flex;
  align-items: left;
  justify-content: space-between;
  flex-direction: column;
  box-shadow: 0 0 0.625rem rgba(0, 0, 0, 0.3);
}

.help-modal-header {
  background-color: var(--poke-yellow);
  border-bottom: 0.5rem solid var(--poke-blue);
  background-color: var(--poke-yellow);
  box-sizing: border-box;
  padding: 0;
  width: 100%;
  height: 5rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.help-modal-header p {
  font-size: 2.8rem;
  text-transform: uppercase;
  text-justify: center;
  font-weight: bold;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 1rem 0.7rem 1rem 0.7rem;
}

ul li {
  margin-bottom: 1rem;
}

.instructions-header {
  font-size: 1.2rem;
  text-transform: uppercase;
  font-weight: bold;
  margin: 0;
}

.instructions {
  font-size: 0.8rem;
  margin: 0.3rem;
}

.copyright {
  font-size: 0.6rem;
  text-justify: center;
  text-align: center;
}

a {
  text-decoration: none;
}

hr {
  border: 1px solid var(--poke-blue);
  opacity: 0.7;
}

@media (max-device-width: 428px) {
  .help-modal-content {
    width: 25rem;
    height: 40rem;
  }
}
</style>
