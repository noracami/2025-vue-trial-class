<script setup>
import { products } from '@/assets/week1/data.json';
import { ref } from 'vue';

const productList = ref(products);
const isEditing = ref(false);

const updatePriceManually = (index) => {
  const newPrice = prompt('請輸入新的價格', productList.value[index].price);
  if (newPrice !== null && !isNaN(newPrice)) {
    if (productList.value[index].price < 0) {
      alert('價格不能為負數');
      return;
    }
    productList.value[index].price = parseInt(newPrice);
  } else {
    alert('請輸入有效的數字');
  }
};

const updateStock = (index, change) => {
  const product = productList.value[index];
  if (product.stock + change >= 0) {
    product.stock += change;
  }
};

const updateStockManually = (index) => {
  const newStock = prompt('請輸入新的庫存數量', productList.value[index].stock);
  if (newStock !== null && !isNaN(newStock)) {
    if (newStock < 0) {
      alert('庫存數量不能為負數');
      return;
    }
    productList.value[index].stock = parseInt(newStock, 10);
  } else {
    alert('請輸入有效的數字');
  }
};
</script>

<template>
  <div class="p-6">
    <table class="table">
      <thead>
        <tr class="tr">
          <th scope="col" class="flex justify-between items-center">
            <p>品項</p>
            <p
              class="text-xl cursor-pointer hover:underline p-4 rounded-2xl"
              :class="{ 'bg-green-700': isEditing }"
              @click="isEditing = !isEditing"
            >
              {{ isEditing ? '完成' : '編輯' }}
            </p>
          </th>
          <th scope="col">描述</th>
          <th scope="col" class="text-center">價格</th>
          <th scope="col" class="text-center">庫存</th>
        </tr>
      </thead>
      <tbody>
        <tr
          class="tr"
          v-for="({ name, description, price, stock }, index) in productList"
          :key="name"
        >
          <td
            class=""
            :class="{ 'bg-gray-300 dark:bg-gray-600': isEditing }"
            :contenteditable="isEditing"
          >
            {{ name }}
          </td>
          <td>
            <small>{{ description }}</small>
          </td>
          <td
            class="text-center cursor-pointer hover:bg-amber-100 hover:dark:bg-gray-700"
            @click="updatePriceManually(index)"
          >
            {{ price }}
          </td>
          <td class="flex justify-between items-center">
            <button class="button" @click="updateStock(index, -1)">-</button>
            <p
              @click="updateStockManually(index)"
              class="grow text-center cursor-pointer hover:underline"
            >
              {{ stock }}
            </p>
            <button class="button" @click="updateStock(index, 1)">+</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
@reference '../assets/main.css';

.table {
  @apply w-full text-left text-4xl border border-gray-200 dark:border-gray-700;
}
.tr {
  @apply border-b border-gray-200 dark:border-gray-700;

  > th {
    @apply px-6 py-4 font-medium text-gray-900 dark:text-gray-100;
  }

  > td {
    @apply px-6 py-4 text-gray-700 dark:text-gray-300;
  }
}

.button {
  @apply text-gray-700 dark:text-gray-300 bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600 p-2 rounded cursor-pointer;
}
</style>
