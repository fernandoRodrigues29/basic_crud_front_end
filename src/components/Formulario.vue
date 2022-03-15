<template>
  <div>
    <div class="container mb-5">
      <h3>Livro de Atos</h3>
      <h4>Componentes</h4>
      
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Atividade</label>
          <input type="text" name="nome" v-model="ataDia.titulo" class="form-control">        
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Dia</label>
          <input type="date" name="dia" v-model="ataDia.dia"   class="form-control">        
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Local</label>
          <input type="text" name="email" v-model="ataDia.local"   class="form-control">        
        </div>
      </div>
      <div class="row mt-3">
        <div class="col">
          <label class="form-label" for="">Atividades</label>
          <textarea class="form-control" v-model="ataDia.atividade" ></textarea>        
        </div>
      </div>
      <div class="row">
        <div class="col">
          <div class="gap-2">
            <button id="butao_cad" class="mt-5 btn btn-success btn-lg" v-on:click="addAta(ataDia)" >Cadastrar</button> 
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <ul class="list-group">
            <li class="list-group-item list-group-item-light" v-for="item in listaAtas" v-bind:key="item">
              {{item.titulo}} - {{item.atividade}}
            </li>
          </ul>
        </div>
      </div>
    </div>  
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import "bootstrap/dist/css/bootstrap.css";
export default {
  name: 'App',
  data(){
       return {
        ataDia:{
          titulo:"",
          dia:"",
          local:"",
          atividade:""
        },
        listaAtas:[],
      };
  },
  methods:{
    addAta(ad){
      this.listaAtas.push(ad);
    }
  },
  components: {
    // HelloWorld
  }
}
</script>

<style>
  #butao_cad{
    width: 100%;
  }
</style>
