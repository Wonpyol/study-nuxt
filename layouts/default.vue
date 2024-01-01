<template>
  <div>
    <h1>{{ $route.name }}</h1>
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