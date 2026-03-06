<template>
  <div>
    <h1>Create Product</h1>

    <form v-on:submit.prevent="createProduct">

      <p>name: <input type="text" v-model="product.name"></p>

      <p>description: <input type="text" v-model="product.description"></p>

      <p>price: <input type="number" v-model="product.price"></p>

      <p>stock: <input type="number" v-model="product.stock"></p>

      <p>
        <button type="submit">create product</button>
      </p>

    </form>
  </div>
</template>

<script>
import ProductsService from '../../services/ProductsService'

export default {
  data () {
    return {
      product: {
        name: '',
        description: '',
        price: '',
        stock: ''
      }
    }
  },

  methods: {
    async createProduct () {
      try {
        await ProductsService.post(this.product)

        this.$router.push({
          name: 'products'
        })
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>