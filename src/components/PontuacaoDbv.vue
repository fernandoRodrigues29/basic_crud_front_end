<template>
  <div>
    <div class="container mb-5">
      <h3>Pontuação do Desbravador</h3>
     
      
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Desbravador</label>
           <input type="text" name="nome" v-model="pontuacao.dbv" class="form-control">
                
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for=""> Presença 
            <span class="badge bg-success">{{pontuacao.presenca}}</span>
          </label>
           <input type="range" v-model="pontuacao.presenca" class="form-range" min="0" max="5" id="customRange2">     </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Pontualidade <span class="badge bg-success">{{pontuacao.pontualidade}}</span></label>
            <input type="range" v-model="pontuacao.pontualidade" class="form-range" min="0" max="5" id="customRange2"> 
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">E Batiado <span class="badge bg-success">{{pontuacao.batizado}}</span></label>
            <input type="range" v-model="pontuacao.batizado" class="form-range" min="0" max="1" id="customRange2"> 
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Horario <span class="badge bg-success">{{pontuacao.horario}}</span></label>
            <input type="range" v-model="pontuacao.horario" class="form-range" min="0" max="5" id="customRange2"> 
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Tarefas da Classe <span class="badge bg-success">{{pontuacao.tarefas_classe}}</span></label>
            <input type="range" v-model="pontuacao.tarefas_classe" class="form-range" min="0" max="5" id="customRange2"> 
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Tarefas da Unidade <span class="badge bg-success">{{pontuacao.tarefas_unidade}}</span></label>
            <input type="range" v-model="pontuacao.tarefas_unidade" class="form-range" min="0" max="5" id="customRange2"> 
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Asseio <span class="badge bg-success">{{pontuacao.asseio}}</span></label>
            <input type="range" v-model="pontuacao.asseio" class="form-range" min="0" max="5" id="customRange2"> 
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label class="form-label" for="">Uniforme <span class="badge bg-success">{{pontuacao.uniforme}}</span></label>
            <input type="range" v-model="pontuacao.uniforme" class="form-range" min="0" max="5" id="customRange2"> 
        </div>
      </div>
      <div class="row">
        <div class="col">
          <div class="gap-2">
            <button id="butao_cad" class="mt-5 btn btn-success btn-lg" v-on:click="addAta(pontuacao)" >Cadastrar</button> 
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <ul class="list-group">
            <li class="list-group-item list-group-item-light" v-for="item in listaAtas" v-bind:key="item">
              {{item.dbv}} | {{item.pontualidade}}  
              | {{item.presenca}} | {{item.batiado}} 
              | {{item.horario}} | {{item.tarefas_classe}}
              | {{item.tarefas_unidade}} | {{item.asseio}}
              | {{item.uniforme}}
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
          pontuacao:{
            dbv:"",
            pontualidade:"",
            presenca:"",
            batizado:"",
            horarios:"",
            tarefas_classe:"",
            tarefas_unidade:"",
            asseio:"",
            uniforme:"",
          },
          listaAtas:[],
      };
  },
  methods:{
    addAta(ad){
      const novoObj = Object.assign({},ad);
      this.listaAtas.push(novoObj);
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
