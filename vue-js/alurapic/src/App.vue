

<template>
  <div class="corpo">

    <h1 class="centralizado">{{ titulo }}</h1>

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto in fotos">
         <meu-painel :foto ="foto.titulo">
           <img class='imagem-responsiva' :src="foto.url" :alt="foto.titulo">
          </meu-painel>
      </li>
    </ul>

  </div>
  
</template>

<script>

import Painel from './components/shared/painel/Painel.vue';

export default {


components:{

    'meu-painel' : Painel
  
  },

    data() {

    return{
      titulo: 'Alurapic',
      fotos:[]
}
    },

    created(){

      let promise = this.$http.get('http://localhost:3000/v1/fotos')
     .then(res => res.json())
     .then(fotos => this.fotos = fotos, err => console.log(err)); 

    }
  }


</script>

<style>
  /* estilo pagina */
  .corpo{
  margin: 0 auto;
  font-family: Arial, Helvetica, sans-serif;
  width: 96%;

}

.centralizado{

  text-align: center;
}

.lista-fotos{

  list-style: none;

}

.lista-fotos .lista-fotos-item{

  display: inline-block;

}
/* fim do estilo pagina */

/* estilo imagem */

.imagem-responsiva {
    width: 100%;
  }  

</style>
