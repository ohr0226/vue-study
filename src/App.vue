<template>
  <div
    class="nav d-flex flex-wrap justify-content-center py-3 mb-4 border-bottom"
  >
    <a class="nav-link" href="" v-for="(item, index) in menu" :key="index">
      {{ item }}
    </a>
  </div>
  <DiscountComponent v-if="isShow === true" />
  <div class="tab-wrapper d-flex justify-content-center">
    <ul class="tab-list d-flex w-25 justify-content-evenly">
      <li>
        <button class="btn btn-primary" @click="priceSort">가격순</button>
      </li>
      <li>
        <button class="btn btn-primary" @click="priceSortReverse">
          가격역순
        </button>
      </li>
      <li>
        <button class="btn btn-primary" @click="priceSortString">
          가나다순
        </button>
      </li>
      <li>
        <button class="btn btn-primary" @click="sortBack">되돌리기</button>
      </li>
    </ul>
  </div>
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
      isShow: true,
      menu: ["HOME", "ABOUT", "PRODUCTS"],
      products: data,
      productOriginData: [...data], // data 원본 카피를 위해 ...로 뿌려서 새 배열로 담아준다.
    };
  },
  mounted() {
    // lifecycle hooks
    // setTimeout(() => {
    //   this.isShow = false;
    // }, 1000);
  },
  methods: {
    openModal(index) {
      this.isOpen = true;
      this.index = index;
    },
    increase(index) {
      this.products[index].report++;
    },
    priceSort() {
      this.products.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceSortReverse() {
      this.products.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    priceSortString() {
      this.products.sort(function (a, b) {
        return a.title.localeCompare(b.title);
      });
    },
    sortBack() {
      this.products = [...this.productOriginData];
      // array 값을 공유달라는 뜻이 되어버림. 여기서도 카피본을 만들어주어야함
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
