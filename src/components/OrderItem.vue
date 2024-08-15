<script setup>
import { defineProps, computed } from 'vue'

const props = defineProps(['orderList', 'orderNote'])

// 購物車總金額
const orderTotalAmount = computed(() => {
  return props.orderList.reduce((p, item) => p + item.price * item.quantity, 0)
})
</script>

<template>
  <div v-if="orderList.length == 0" class="alert alert-secondary text-center" role="alert">
    尚未建立訂單
  </div>
  <div v-else class="card">
    <div class="card-body">
      <div class="card-title">
        <h5>訂單</h5>
        <table class="table">
          <thead>
            <tr>
              <th scope="col">品項</th>
              <th scope="col">數量</th>
              <th scope="col">小計</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="orderItem in orderList" :key="orderItem.id">
              <td>{{ orderItem.name }}</td>
              <td>{{ orderItem.quantity }}</td>
              <td>{{ orderItem.quantity * orderItem.price }}</td>
            </tr>
          </tbody>
        </table>
        <div class="text-end">
          備註: <span>{{ orderNote }}</span>
        </div>
        <div class="text-end">
          <h5>
            總計: <span>${{ orderTotalAmount }}</span>
          </h5>
        </div>
      </div>
    </div>
  </div>
</template>
