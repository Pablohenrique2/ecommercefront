<template>
  <section class="bg-[url('../../public/img/capaLogin.jpg')] h-[623px] flex justify-center items-center">
    <div class="bg-[#fff159] cursor-pointer">
      <p @click="redirectToMercadoLivre()" class="p-[20px]">Entrar na Loja</p>
    </div>
  </section>
</template>

<script>
// import api from '../plugins/api';

export default {
  name: 'LoginView',

  methods: {
    redirectToMercadoLivre() {
      const clientId = '8120965250227328';
      const redirectUri = 'http://localhost:8000/auth/mercado-livre/callback';
      const authorizationUrl = `https://auth.mercadolivre.com.br/authorization?response_type=code&client_id=${clientId}&redirect_uri=${redirectUri}`;
      window.location.href = authorizationUrl;
      this.$router.push('/home');
    },
  },
}
</script>