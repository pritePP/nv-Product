<template>
  <div>
    <h2>Get all products</h2>

    <p><button v-on:click="logout()">Logout</button></p>

    <p>
      <button v-on:click="navigateTo('/product/create')">
        สร้าง Product
      </button>
    </p>

    <h4>จำนวนสินค้า {{ products.length }}</h4>

    <div v-for="product in products" :key="product.id">

      <p>id: {{ product.id }}</p>
      <p>name: {{ product.name }}</p>
      <p>description: {{ product.description }}</p>
      <p>price: {{ product.price }}</p>
      <p>stock: {{ product.stock }}</p>

      <p>
        <button v-on:click="navigateTo('/product/' + product.id)">
          ดูข้อมูล
        </button>
      </p>

      <p>
        <button v-on:click="navigateTo('/product/edit/' + product.id)">
          แก้ไขข้อมูล
        </button>
      </p>

      <p>
        <button v-on:click="deleteProduct(product)">
          ลบข้อมูล
        </button>
      </p>

      <hr>

    </div>
  </div>
</template>

<script>
import ProductsService from '../../services/ProductsService'
import { useAuthenStore } from '../../stores/authen'

export default {
  data () {
    return {
      products: []
    }
  },

  async created () {
    try {
      this.products = (await ProductsService.index()).data
    } catch (error) {
      console.log(error)
    }
  },

  methods: {
    navigateTo (route) {
      this.$router.push(route)
    },

    async deleteProduct (product) {
      const result = confirm("ต้องการลบข้อมูลหรือไม่?")
      if (result) {
        await ProductsService.delete(product)
        this.refreshData()
      }
    },

    async refreshData () {
      this.products = (await ProductsService.index()).data
    },

    logout () {
      const authenStore = useAuthenStore()
      authenStore.logout()

      this.$router.push({
        name: 'login'
      })
    }
  }
}
</script>