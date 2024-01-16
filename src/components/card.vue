<template>
  <li class="mb-5">
    <div class="item-click">
      <img
        :src="item.img.src"
        :alt="item.img.alt"
        class="w-100 mb-3"
        @click="$emit('openModal', index)"
      />
      <h4>
        <span>{{ index + 1 + "." }}</span>
        {{ item.title }}
      </h4>
      <strong class="d-block my-3">{{ item.price }}만원</strong>
      <button class="btn btn-danger me-2" @click="$emit('isIncrease')">
        허위매물신고</button
      ><span>신고수 : {{ item.report }}</span>
    </div>
  </li>
</template>
<script>
export default {
  name: "CardComponent",
  props: {
    item: Object,
    index: Number,
  },
};
</script>
<style></style>
