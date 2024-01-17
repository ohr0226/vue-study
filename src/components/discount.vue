<template>
  <div class="discount">
    <h4>지금 결제하면 {{ discount }}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: "DiscountComponent",
  data() {
    return {
      discount: 5,
    };
  },
  mounted() {
    const interval = setInterval(() => {
      this.discount--;
      if (this.discount === 0) {
        clearInterval(interval);
      }
    }, 1000);
  },
};
</script>
<style>
.discount {
  background: #eee;
  padding: 30px;
  margin: 20px;
  border-radius: 5px;
  text-align: center;
  h4 {
    margin: 0;
  }
}
</style>
