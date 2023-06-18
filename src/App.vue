<template>
  <nav v-if="isHomeRoute" class="bg-[#fff159] h-[60px] flex items-center justify-between px-[20px]">
    <img src="../public/img/logo-site.png" class="w-[150px]" alt="">
    <div>
      <router-link to="/home">Produtos</router-link> |
      <router-link to="/cadastrar">cadastrar</router-link>
    </div>
  </nav>
  <router-view/>
</template>

<script>
export default {
  name: 'App',
  computed: {
    isHomeRoute() {
      return this.$route.path !== '/';
    }
  }
};
</script>

<style>

</style>
