<script setup lang="ts">
import { reactive, ref, computed, watch, toRefs } from "vue";

// const itemName1 = ref<string>("Desk");

const item1 = reactive({
  name: "Desk",
  price: 4000,
  url: "http://google.com",
});

const buy = (itemName: string) => {
  alert("Are you sure to buy" + itemName);
};

const clear = () => {
  item1.name = "";
  item1.price = 0;
};

const budget = 50000;

// const priceLabel = computed(() => {
//   if (item1.price > budget) {
//     return "too expensive";
//   } else {
//     return item1.price + "yen";
//   }
// });
const priceLabel = ref<string>(item1.price + " yen");
const { price } = toRefs(item1);
watch(price, () => {
  if (price.value > budget) {
    priceLabel.value = "too expensive";
  } else {
    priceLabel.value = price.value + "yen";
  }
});
</script>

<template>
  <div class="container">
    <h1>Payment</h1>
    <input v-model="item1.name" />
    <input v-model="item1.price" />
    <button v-on:click="clear">Clear</button>
    <div class="payment">
      <label>{{ item1.name }}</label>
      <label>{{ priceLabel }}</label>
      <button v-on:click="buy(item1.name)">BUY</button>
    </div>
  </div>
</template>

<style scoped>
label {
  font-size: 20px;
  font-weight: bold;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background: aliceblue;
}
</style>
