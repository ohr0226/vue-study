<template>
  <div class="discount">
    <h4>{{ banner }}</h4>
  </div>
</template>

<script>
export default {
  name: "DiscountComponent",
  data() {
    return {
      banner: "지금 결제하면 20% 할인",
    };
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
