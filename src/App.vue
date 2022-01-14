<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link
        to="/"
        class="top-bar-link"
      >
        <i class="icofont-spoon-and-fork" />
        <span>Home</span>
      </router-link>
      <router-link
        to="/products"
        class="top-bar-link"
      >
        <span>Products</span>
      </router-link>
      <router-link
        to="/past-orders"
        class="top-bar-link"
      >
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div
      class="top-bar-cart-link"
      @click="toggleSidebar"
    >
      <i class="icofont-cart-alt icofont-1x" />
      <span>Cart ( {{ totalQuantity }} )</span>
    </div>
  </header>
  <router-view
    :inventory="inventory"
    :add-to-cart="addToCart"
  />
  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />
</template>
<script>
import Sidebar from './components/Sidebar.vue'
import inventory from '@/food.json'

export default {
  components: {
    Sidebar
  },

  data () {
    return {
      showSidebar: false,
      inventory: inventory,
      cart: {}
    }
  },
  computed: {

    totalQuantity () {
      const numArr = Object.values(this.cart)
      return numArr.reduce((acc, cur) => {
        // eslint-disable-next-line no-return-assign
        return acc += cur
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (name) {
      delete this.cart[name]
    }
  }
}
</script>
