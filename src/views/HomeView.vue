<script>
import axios from 'axios';

export default {
  name: 'Serie',
  initPath: "",
  data() {
    return {
      serie: Array, 
    }
  },  
  created() { //ciclo de vida quando cria o componente/pagina
    this.getSerieRandom();
  },
  methods: {
    async getSerieRandom() {
       
      let urlPath = 'http://127.0.0.1:8000/api/get-register-random';
      await axios.get(urlPath).then(
        (response) => {
          console.log(response.data[0]);

          if(response.status == 200) {
            this.serie = response.data[0]; 
            this.initPath = "http://localhost:8000/storage/" + this.serie?.livros[0]?.capa;
            this.titleLivro = this.serie?.livros[0]?.nome;
          }
          
        }
      ).catch((err) => {

        console.log(err);
      
      }); 

    }
  },

}

</script>

<template>
  <main>
    <div class="bg-white py-24 sm:py-32">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl lg:text-center">
        <h2 class="text-base font-semibold leading-7 text-indigo-600">{{ serie?.id }}</h2>
        <p class="mt-2 text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">{{ serie?.nome }}</p>
        <p class="mt-6 text-lg leading-8 text-gray-600">{{ serie?.livros[0]?.nome }}</p> 
        <!-- {{ serie }} -->
        <img :src="initPath" style="width: 350px;height: 500px;" :alt="serie?.livros[0]?.nome" >
      </div>
    </div>
  </div>
  </main>
</template>
