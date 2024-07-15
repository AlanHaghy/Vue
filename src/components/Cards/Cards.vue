<script>

export default {
  name:'Cards',
  props: ["title",
    "priceTag",
    "nonRefundable",
    "isError",
    "selected",
    "caption",
    "req"],
}
</script>

<template>
  <div
   :class="['ecard', { error: isError }, {selected:selected}]">
    <div class="title">
      <div class="title-text">{{ title }}</div>
      <div class="price-tag">{{ priceTag == 0 ? 'Free' : '$'+ priceTag }}</div>
      <div class="refundable">{{ nonRefundable ? "non-refundable" : "" }}</div>
      <div class="caption">{{ caption }}</div>
    </div>
    <div class="context">
      <div class="reqTitle">Requirements</div>
      <ul>
        <li v-for="item in req" :key="item.name">{{ item }}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
@import "./style.scss";
</style>
