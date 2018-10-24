<!-- alurapic/src/App.vue -->
<template>
  <div class="corpo">

  <h1 class="centralizado">Alurapic</h1>

  <input type="search" class='filtro' @input='filtro = $event.target.value' placeholder="filtre pelo titulo">
    <ul class="lista-fotos">

      <li class="lista-fotos-item" v-for="(foto, index) in fotosComFiltro" :key="index">

        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url='foto.url' :titulo='foto.titulo'></imagem-responsiva>

          <meu-botao rotulo='remover'
           tipo='button'
           :confirmacao='true'
           estilo="perigo"
            @botaoAtivado="remove(foto)"/>

        </meu-painel>

      </li>
    </ul>

  </div>
</template>

<script>

// importando nosso Painel 

import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/imagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue';


export default {

methods: {

    remove(foto) {
      // exibindo o título da foto selecionado
      alert(foto.titulo);
    }
  },

components:{

    'meu-painel' : Painel,
    'imagem-responsiva' : ImagemResponsiva,
    'meu-botao': Botao 
  },


    data() {

    return{
      fotos:[],
      filtro: ''
}
    },

    computed:{

      fotosComFiltro(){

      if (this.filtro) {
          

        let exp = new RegExp(this.filtro.trim(), 'i');
       

        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }

      }

    },

created() {

    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}


</script>

<style>
  /* estilo pagina */

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

.filtro {
    display: block;
    width: 100%;
  }

</style>
