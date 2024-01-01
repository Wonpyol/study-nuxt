<template>
  <div>
    <ul>
      <li>메인페이지 입니다.</li>
    </ul>
    <div>{{ products }}</div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      products: [],
    }
  },

  async created() { //컴포넌트가 생성된기 이전에 호출됨
    const response = await axios.get("http://localhost:3000/products");
    console.log(response.data)
    this.products = response.data;
  },
}
</script>