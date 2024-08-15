<script setup>
import { ref, defineProps, defineEmits, computed } from 'vue'
const props = defineProps(['cartList'])

const emit = defineEmits(['delteCartItem', 'sendOrder'])

const note = ref('')

// 購物車總金額
const totalAmount = computed(() => {
  return props.cartList.reduce((p, item) => p + item.price * item.quantity, 0)
})

const emitSendOrder = () => {
  emit('sendOrder', note.value)
  note.value = ''
}
</script>
<template>
  <table class="table">
    <thead>
      <tr>
        <th scope="col" width="50">操作</th>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col" width="90">數量</th>
        <th scope="col">單價</th>
        <th scope="col">小計</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="cartItem in cartList" :key="cartItem.id">
        <td>
          <button type="button" class="btn btn-sm" @click="emit('delteCartItem', cartItem.id)">
            x
          </button>
        </td>
        <td>{{ cartItem.name }}</td>
        <td>
          <small>{{ cartItem.description }}</small>
        </td>
        <td>
          <select class="form-select" v-model="cartItem['quantity']">
            <option :value="i" v-for="i in 10" :key="i">{{ i }}</option>
          </select>
        </td>
        <td>{{ cartItem.price }}</td>
        <td>{{ cartItem.quantity * cartItem.price }}</td>
      </tr>
    </tbody>
  </table>

  <div class="alert alert-primary text-center" role="alert" v-if="cartList.length == 0">
    請選擇商品
  </div>
  <div v-else>
    <div class="text-end mb-3">
      <h5>
        總計: <span>${{ totalAmount }}</span>
      </h5>
    </div>
    <textarea class="form-control mb-3" rows="3" placeholder="備註" v-model="note"></textarea>
    <div class="text-end">
      <button class="btn btn-primary" @click="emitSendOrder">送出</button>
    </div>
  </div>
</template>
