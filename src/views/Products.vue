<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <ProductCard
        v-for="(product) in inventory.slice(0, 6)"
        :key="product.id"
        :product="product"
        :add-to-cart="addToCart"
        class="card"
      />
    </div>
  </main>
</template>

<script>
import ProductCard from '../components/ProductCard.vue'

export default {
  components: { ProductCard },
  props: ['addToCart', 'inventory']
}
</script>
