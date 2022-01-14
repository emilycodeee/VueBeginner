<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x" />
        </span>
        <button
          class="cart-close"
          @click="toggle"
        >
          &times;
        </button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(quantity,key,value,i) in cart"
              :key="i"
            >
              <td><i class="icofont-carrot icofont-3x" /></td>
              <td>{{ key }}</td>
              <td>$ {{ getPrice(key) }}</td>
              <td class="center">
                {{ quantity }}
              </td>
              <td>$ {{ quantity * getPrice(key) }}</td>
              <td class="center">
                <button
                  class="btn btn-light cart-remove"
                  @click="remove(key)"
                >
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p
          v-if="!Object.keys(cart).length"
          class="center"
        >
          <em>No items in cart</em>
        </p>
        <div class="spread">
          <span><strong>Total:</strong> ${{ caculateTotal() }}</span>
          <button class="btn btn-light">
            Checkout
          </button>
        </div>
      </div>
    </div>
  </aside>
</template>
<script>
export default {
  props: ['toggle', 'cart', 'inventory', 'remove'],
  methods: {
    getPrice (name) {
      const p = this.inventory.find((item) => item.name === name)
      const price = p.price.USD
      return price
    },
    caculateTotal () {
      let total = 0
      for (const [key, value] of Object.entries(this.cart)) {
        total += this.getPrice(key) * value
      }
      return total.toFixed(2)
    }

  }
}
</script>
