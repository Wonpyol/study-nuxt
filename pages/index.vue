<template>
  <div class="app">
    <SearchInput v-model="inputText" @search="searchProduct"></SearchInput>
    <main>
      <ul>
        <li
            v-for="product in products"
            :key="product.id"
            class="item flex"
            @click="routeToDetailPage(product.id)"
        >
            <p>{{ product.name }}</p>
            <p>{{ product.name }}</p>
            <p>{{ product.price }}</p>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
import axios from "axios";
import SearchInput from "@/components/SearchInput.vue";
import {fetchProductsByKeyword} from "@/api/index";
export default {
  components: {SearchInput},
  data() {
    return {
      products: [],
      inputText: '' //프롭스 받을곳
    }
  },

  async created() {
    const response = await axios.get("http://localhost:3000/products");
    this.products = response.data.map((product) => {
      return {
        ...product,
        imageUrl : `${product.imageUrl}?random=${Math.random()}`
      }
    })
  },
  methods: {
    routeToDetailPage(id) {
      this.$router.push(`/detail/${id}`);
    },
    async searchProduct() {
      console.log(this.inputText);
      let response = await fetchProductsByKeyword(this.inputText);

      this.products = response.data.map((product) => {
        return {
          ...product,
          imageUrl : `${product.imageUrl}?random=${Math.random()}`
        }
      })

    },
  }
}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}
.item {
  display: inline-block;
  width: 400px;
  height: 300px;
  text-align: center;
  margin: 0 0.5rem;
  cursor: pointer;
}
.product-image {
  width: 400px;
  height: 250px;
}
.app {
  position: relative;
}
.cart-wrapper {
  position: sticky;
  float: right;
  bottom: 50px;
  right: 50px;
}
.cart-wrapper .btn {
  display: inline-block;
  height: 40px;
  font-size: 1rem;
  font-weight: 500;
}
</style>