<template>
  <div class="px-[30px]">
    <div class="text-center">
      <p>Cadastrar Produto</p>
    </div>
    <label for="large-input" class="block mb-2 text-sm font-medium text-black ">titulo</label>
    <input type="text" v-model="titulo" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400  dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="mesa" required>
    <label for="large-input" class="block mb-2 text-sm font-medium text-black  ">categoria</label>
    <select v-model="selectedCategory"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
      <option value="">Selecione uma categoria</option>
      <option v-for="category in listCategory" :value="category.id" :key="category.id">{{ category.name }}</option>
    </select>
    <label for="large-input" class="block mb-2 text-sm font-medium text-black ">price</label>
    <input type="text" v-model="price"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400  dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="preço" required>
    <label for="large-input" class="block mb-2 text-sm font-medium text-black  ">quantidade</label>
    <input type="text" v-model="quantidade"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="quatidade" required>
    <label for="large-input" class="block mb-2 text-sm font-medium text-black  ">imagem</label>
    <input type="text" v-model="img"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="imagem" required>
    <button type="button" @click="createProduct()" class="focus:outline-none text-white bg-green-700 hover:bg-green-800 focus:ring-4 focus:ring-green-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800">cadastrar</button>
  </div>
</template>

<script>
import api from '../plugins/api';

export default {
  name: 'Cadastrar-Product',
  data() {
    return {
      listCategory: [],
      selectedCategory: '',
      titulo: '',
      price: '',
      quantidade: '',
      img: ''
    };
  },
  beforeMount() {
    this.getCategory();
  },
  methods: {
    async getCategory() {
      api.get('/listCategory')
        .then(response => {
          this.listCategory = response.data; 
        });
    },
    async createProduct() {
      var data = {
        titulo: this.titulo,
        price: this.price,
        quantidade: this.quantidade,
        selectedCategory: this.selectedCategory,
        img: this.img
      };
      console.log(data);
      api.post('/addProduct', data)
        .then(response => {
          console.log(response.data);
          this.$router.push('/home');
        });
    },
    formatPrice(price) {
      return price.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
    },
  },
}
</script>

