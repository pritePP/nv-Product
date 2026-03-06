<template>
  <div>
    <h1>Edit Product</h1>

    <form v-on:submit.prevent="editProduct">

      <p>name: <input type="text" v-model="product.name"></p>

      <p>description: <input type="text" v-model="product.description"></p>

      <p>price: <input type="number" v-model="product.price"></p>

      <p>stock: <input type="number" v-model="product.stock"></p>

      <p>
        <button type="submit">edit product</button>
      </p>

    </form>
  </div>
</template>

<script>
import ProductsService from '../../services/ProductsService'

export default {
  data () {
    return {
      product: {}
    }
  },

  async created () {
    try {
      this.product = (await ProductsService.show(this.$route.params.id)).data
    } catch (error) {
      console.log(error)
    }
  },

  methods: {
    async editProduct () {
      try {
        await ProductsService.put(this.product)

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