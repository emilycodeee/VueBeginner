<template>
  <div

    :key="product.id"
    class="card"
  >
    <div class="card-title">
      {{ product.name }}
    </div>
    <div class="card-body">
      <i class="icofont-10x icofont-{{Product.icon}}" />
      <form>
        <div class="row">
          <div class="cell">
            <label>Type:</label>
          </div>
          <div class="cell">
            <em>{{ product.type }}</em>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Price:</label>
          </div>
          <div class="cell">
            ${{ product.price.USD }}
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Quantity:</label>
          </div>
          <div class="cell">
            <input
              v-model.number="quantity"
              type="number"
            >
          </div>
        </div>
      </form>
    </div>
    <div class="card-footer">
      <button
        class="btn btn-light"
        @click="addToCart(product.name, quantity)"
      >
        Add to cart
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: [

    'product', 'addToCart'
  ],
  data () {
    return {
      quantity: 0
    }
  }
}
</script>
