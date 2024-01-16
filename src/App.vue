<template>
  <div
    class="nav d-flex flex-wrap justify-content-center py-3 mb-4 border-bottom"
  >
    <a class="nav-link" href="" v-for="(item, index) in menu" :key="index">
      {{ item }}
    </a>
  </div>
  <DiscountComponent />
  <Transition name="fade">
    <ModalComponent
      v-bind:products="products"
      v-bind:isOpen="isOpen"
      v-bind:index="index"
      @openModal="isOpen = false"
      v-show="isOpen"
    />
  </Transition>
  <div class="d-flex flex-wrap flex-column align-items-center text-center">
    <ul class="w-50 list-item">
      <CardComponent
        v-for="(item, index) in products"
        :key="index"
        v-bind:item="item"
        v-bind:index="index"
        @openModal="
          isOpen = true;
          openModal($event);
        "
        @isIncrease="increase(index)"
      />
    </ul>
  </div>
</template>

<script>
import data from "@/data";
import DiscountComponent from "@/components/discount.vue";
import ModalComponent from "@/components/modal.vue";
import CardComponent from "@/components/card.vue";
// ref, reactive
export default {
  name: "App",
  data() {
    return {
      index: 0,
      isOpen: false,
      menu: ["HOME", "ABOUT", "PRODUCTS"],
      products: data,
    };
  },
  methods: {
    openModal(index) {
      this.isOpen = true;
      this.index = index;
    },
    increase(index) {
      this.products[index].report++;
    },
  },
  components: {
    CardComponent: CardComponent,
    DiscountComponent: DiscountComponent,
    ModalComponent: ModalComponent,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  /*margin-top: 60px;*/
  ul {
    padding: 0;
  }
  li {
    list-style: none;
  }
  a {
    text-decoration: none;
    color: #000;
  }
  img {
    cursor: pointer;
  }

  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity 1s;
  }
  .fade-enter-to {
    opacity: 1;
  }
}
</style>
