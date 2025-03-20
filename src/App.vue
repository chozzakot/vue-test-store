<script setup>
import { computed, onMounted, provide, ref, watch } from 'vue'
import axios from 'axios'

import Header from './components/Header-component.vue'
import CardList from './components/CardList-component.vue'
import Drawer from './components/Drawer-component.vue'

const items = ref([])
const cart = ref([])

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))

const drawerOpen = ref(false)

const openDrawer = () => {
  drawerOpen.value = true
}

const closeDrawer = () => {
  drawerOpen.value = false
}

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)

  const itemIndex = items.value.findIndex(({ id }) => id === item.id)
  if (itemIndex !== -1) {
    items.value[itemIndex].isAdded = false
  }
}

const onClickPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
}

onMounted(async () => {
  try {
    const { data } = await axios.get('https://dff36f8c545aa7bb.mokky.dev/items')

    items.value = data
  } catch (err) {
    console.log(err)
  }

  const localCart = localStorage.getItem('cart')
  cart.value = localCart ? JSON.parse(localCart) : []

  items.value.forEach((item) => {
    item.isAdded = cart.value.some((cartItem) => cartItem.id === item.id)
  })
})

watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  {
    deep: true,
  },
)

provide('cart', {
  cart,
  addToCart,
  removeFromCart,
})
</script>

<template>
  <Drawer v-if="drawerOpen" :closeDrawer="closeDrawer" :totalPrice="totalPrice" />

  <div class="bg-white w-4/5 m-auto rounded-t-xl shadow-xl mt-14">
    <Header :totalPrice="totalPrice" :openDrawer="openDrawer" />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>
      </div>
      <CardList :items="items" @addToCart="onClickPlus" />
    </div>
  </div>
</template>

<style scoped></style>
