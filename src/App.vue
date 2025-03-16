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

/* const sortBy = ref('')
const onChangeSelect = (event) => {
  sortBy.value = event.target.value
} */

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAdded = false
}

const onClickPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
  console.log(cart)
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

  items.value = items.value.map((item) => ({
    ...item,
    isAdded: cart.value.some((cartItem) => cartItem.id === item.id),
  }))
})

/* watch(sortBy, async () => {
  try {
    const { data } = await axios.get(
      'https://dff36f8c545aa7bb.mokky.dev/items?sortBy=' + sortBy.value,
    )

    items.value = data
  } catch (err) {
    console.log(err)
  }
}) */

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

        <!-- select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
          <option value="name">По названию (A-Z)</option>
          <option value="price">Сначала дешевле</option>
          <option value="-price">Сначала дороже</option>
        </select -->
      </div>
      <CardList :items="items" @addToCart="onClickPlus" />
    </div>
  </div>
</template>

<style scoped></style>
