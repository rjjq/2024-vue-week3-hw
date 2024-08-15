<script setup>
import { ref } from 'vue'

import ProductList from '@/components/ProductList.vue'
import CartItem from '@/components/CartItem.vue'
import OrderItem from '@/components/OrderItem.vue'

const data = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60
  }
])

// 加入購物車
const cartList = ref([])
const addCart = (product) => {
  const index = cartList.value.findIndex((item) => item.id === product.id)
  if (index == -1) {
    cartList.value.push({ ...product, ['quantity']: 1 })
  }
}

// 移除購物車
const delteCartItem = (id) => {
  const index = cartList.value.findIndex((item) => item.id === id)
  if (index !== -1) {
    cartList.value.splice(index, 1)
  }
}

const orderList = ref([])
const orderNote = ref('')
// 送出訂單
const sendOrder = (note) => {
  orderList.value = [...cartList.value]
  orderNote.value = note

  // 清除購物車
  cartList.value = []
}
</script>

<template>
  <div id="root">
    <div class="container mt-5">
      <div class="row">
        <ProductList :data="data" @add-cart="addCart" />

        <div class="col-md-8">
          <CartItem
            :cart-list="cartList"
            @delte-cart-item="delteCartItem"
            @send-order="sendOrder"
          />
        </div>
      </div>
      <hr />
      <div class="row justify-content-center">
        <div class="col-8">
          <OrderItem :order-list="orderList" :order-note="orderNote" />
        </div>
      </div>
    </div>
  </div>
</template>
