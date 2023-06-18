<template>
  <section>
    <div>
      <img src="../../public/img/capa-home.jpg"  class="w-full h-[400px]" alt="" srcset="">
    </div>
    <div class="flex  gap-x-3.5 justify-center py-[10px]">
      <div>
        <p>Pagamento rápido e seguro</p>
      </div>
      <div>
        <p>Até 10 parcelas sem juros</p>
      </div>
      <div>
        <p>Parcelamento sem cartão</p>
      </div>
      <div>
        <p>Via Pix</p>
      </div>
    </div>
    <div class="flex gap-x-3 px-[10px]">
      <div class="w-[224px] h-[350px] " v-for="item in listProduct" :key="item.id">
        <img :src="item.pictures[0].url" alt="">
        <p>titulo: {{ item.title }}</p>
        <p>categoria: {{ item.category_id }}</p>
        <p>quantidade: {{ item.available_quantity}}</p>
        <p>preço: {{ formatPrice(item.price) }}</p>
      </div>
    </div>
  </section>
</template>

<script>
import api from '../plugins/api';

export default {
  name: 'HomeView',
  data() {
    return {
      listProduct: [],
    };
  },
  beforeMount() {
    this.sendFile();
  },
  methods: {
    async sendFile() {
      api.get('/listProduct')
        .then(response => {
          this.listProduct = response.data;
          console.log(response.data); 
        });
    },
    formatPrice(price) {
      return price.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
    },
  },
}
</script>
