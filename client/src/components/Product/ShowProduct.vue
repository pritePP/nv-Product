<template>
  <div>
    <h1>Show Product</h1>

    <p>ID: {{ product.id }}</p>
    <p>Name: {{ product.name }}</p>
    <p>Description: {{ product.description }}</p>
    <p>Price: {{ product.price }}</p>
    <p>Stock: {{ product.stock }}</p>

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
  }
}
</script>