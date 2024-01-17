<template>
  <div class="modal" :class="{ active: isOpen }">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header flex-column">
          <h2>상세정보</h2>
        </div>
        <div class="modal-body d-flex flex-column justify-content-center">
          <img :src="products[index].img.src" :alt="products[index].img.alt" />
          <h4 class="mt-4">{{ products[index].title }}</h4>
          <p>{{ products[index].description }}</p>

          <p>{{ month }}개월 선택함: {{ products[index].price * month }}만원</p>
          <input v-model.number="month" />
        </div>
        <div class="modal-footer d-flex flex-column">
          <DiscountComponent />
          <button v-on:click="closeModel" class="btn btn-primary mt-4">
            닫기
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import DiscountComponent from "@/components/discount.vue";

export default {
  name: "ModalComponent",
  data() {
    return {
      month: 1,
      text: "입력",
    };
  },
  watch: {
    //특정 데이터가 변경될 때마다 실행되는 코드
    month(data) {
      if (data >= 13) {
        alert("13개월 이하로 작성해주시기 바랍니다.");
      }

      if (typeof data === "string") {
        alert("숫자만 입력해주시기 바랍니다.");
      }
    },
  },
  beforeUpdate() {
    if (this.month === 2) {
      alert("최소 3개월이상 입력하세요.");
      this.month = 3;
    }
  },
  props: {
    products: Array,
    isOpen: Boolean,
    index: Number,
  },
  components: { DiscountComponent },
  methods: {
    closeModel() {
      this.$emit("openModal");
    },
  },
};
</script>
<style>
.modal {
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(5px);
  h2,
  p {
    margin: 0;
  }
}
.modal {
  display: block;
  &.active {
    opacity: 1;
  }
}
.modal-header,
.modal-body,
.modal-footer {
  padding: 20px;
}
.modal-footer {
  button {
    width: 100%;
    margin: 0;
    height: 50px;
  }
}
</style>
