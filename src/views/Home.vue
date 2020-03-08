<template>
  <div class="home">
    <reg-form></reg-form>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {
    RegForm: () => import('@/components/form')
  }
}
</script>

<style lang="scss" scoped>
.home {
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
