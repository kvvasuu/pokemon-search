<template>
  <div class="item-container">
    <div class="item-container-inner">
      <div class="item-caption">ITEMS:</div>
      <div class="items">
        <div
          class="item"
          v-for="(item, index) in items"
          :key="item.name"
          @click="itemTransfer(index), itemModalHandle()"
        >
          <img
            class="item-img"
            :id="item.name"
            :src="item.sprites.default"
            :alt="item.name"
          />
        </div>
      </div>
    </div>
  </div>
  <item-modal
    v-if="itemModalShow"
    @toggle-modal="itemModalHandle"
    :item="currentItem"
  ></item-modal>
</template>

<script>
import ItemModal from "./ItemModal.vue";

export default {
  components: {
    ItemModal,
  },
  props: ["items"],
  data() {
    return { itemModalShow: false, currentItem: "" };
  },
  methods: {
    itemModalHandle() {
      this.itemModalShow = !this.itemModalShow;
    },
    itemTransfer(item) {
      this.currentItem = this.items[item];
      console.dir(this.currentItem);
    },
  },
};
</script>

<style>
.item-caption {
  display: block;
  font-weight: bold;
  font-size: 1.2rem;
  text-shadow: 0.15rem 0.15rem 0.15rem var(--poke-blue);
  color: var(--poke-yellow);
  margin: 0.8rem;
  filter: drop-shadow(0.1rem 0.1rem 0.2rem #222);
}

.item-container {
  background-color: var(--background-transparent);
  color: var(--black);
  border-radius: 0.3rem;
  width: 25rem;
  margin: 1rem 0 0 0;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 0.625rem rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(2px);
}

.item-container-inner {
  background-color: rgba(255, 255, 255, 0.3);
  border-radius: 0.2rem;
  width: 96%;
  height: 96%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0.4rem;
}
.items {
  display: flex;
  align-items: center;
  justify-content: left;
}

.item {
  color: var(--black);
  border-radius: 0.3rem;
  display: flex;
  align-items: center;
  justify-content: left;
  margin: 0 0.2rem 0 0.2rem;
  cursor: pointer;
}

.item-img {
  width: 2.4rem;
  -webkit-filter: drop-shadow(0.1rem 0.2rem 0.2rem #222);
  filter: drop-shadow(0.1rem 0.2rem 0.2rem #222);
}
</style>
