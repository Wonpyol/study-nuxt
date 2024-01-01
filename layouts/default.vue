<template>
  <div>
    <header>
      <h1>{{ $route.name }}</h1>
      <NuxtLink to="/main">메인으로</NuxtLink>
      <NuxtLink to="/product">상품페이지</NuxtLink>
    </header>
    <slot />
  </div>
</template>

<script>
export default {
  name: "default"
}
</script>

<style scoped>

</style>