<template>
    <div>
        <div class="row">
            <div class="col">
                <div class="acao-add">
                    add
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <img src="" alt="">
                </div>
            <div class="col">
                <span>Nome</span>
                <p>
                    classe
                </p>
            </div>
            <div class="col">
                <div class="acao">
                    <div class="editar">editar</div>
                    <div class="excluir">excuir</div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
// import { defineComponent } from '@vue/composition-api'

export default {
 name:"App",
 data(){
     return {
         dbvs:[{
             nome:'',
             img:'',
             id:''
         }]
     }
 },
 methods:{
     addDbv(){
         return '';
     },
     excluirDbv(){
         return '';
     },
     editarDbv(id){
         return '';
     },
     listarDbv(){
         return '';
     }
 },
 components:{

 }
}
</script>
