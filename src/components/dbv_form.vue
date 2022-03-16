<template>
    <div>
        <div class="conteiner-principal">
                <div class="row  lista_desbravadores_conteiner">
                        <div class="cabecalho">
                                <div class="pesquisaBox">
                                <input type="text" class="pesuisa_input" v-on:keyup.enter="pesquisarDbv()" v-model="campo_pesquisa">
                                <button class="pesq_button" v-on:click="pesquisarDbv()"> pesquisar </button>
                                </div>
                                <button class="btn" v-on:click="ocultarDiv">Cadastrar</button>
                        </div>
                        <div class="tabela">
                            <div v-for="(lista,index0) in lista_dbvs" :key="index0" >
                                
                                <div v-if="index0 === pagina_atual">
                                    <div class="linha" v-for="(item,index) in lista" :key="index">
                                            <div class="col-1">
                                                <img :src="item.img" alt="">
                                            </div>  
                                            <div class="col-1">
                                                {{item.nome}}
                                                <span>cargo</span>
                                            </div>  
                                            <div class="col-1"><button  v-on:click="editarFormDbv(item,index)">editar</button></div>  
                                            <div class="col-1"><button  v-on:click="excluirDbv(index)">excluir</button></div>  
                                    </div>
                                </div>
                            </div>
                        </div>
                        <paginate
                            :page-count=paginas_a_ser_paginadas
                            :click-handler="funcao_paaginacao"
                            :prev-text="'Prev'"
                            :next-text="'Next'"
                            :container-class="'ul_paginacao'"
                            :page-class="'page-item'"
                            >
                        </paginate>
                </div>
                <div class="row conteiner_central ocultar_conteudo">
                    <div class="col-12">
                        <div class="form_conteiner">
                            <label for="nome">Nome</label>
                            <input type="text" v-model="dbv.nome" name="nome" id="nome">
                        </div>
                    </div>
                    <!-- <div class="col-12">
                        <div class="form_conteiner">
                            <label for="idade">Idade</label>
                            <input type="text"  v-model="dbv.idade"  name="idade" id="idade">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                            <label for="sexo">Sexo</label>
                            <input type="text"  v-model="dbv.sexo"  name="sexo" id="sexo">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="endereco">Endereço</label>
                        <input type="text"  v-model="dbv.endereco"  name="endereco" id="endereco">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="complemento">Complemento</label>
                        <input type="text"  v-model="dbv.complemento"  name="complemento" id="complemento">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="cidade">Cidade</label>
                        <input type="text"  v-model="dbv.cidade"  name="cidade" id="cidade">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="numero">Numero</label>
                        <input type="text"  v-model="dbv.numero"  name="numero" id="numero">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="bairro">Bairro</label>
                        <input type="text"  v-model="dbv.bairro"  name="bairro" id="bairro">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="estado">Estados</label>
                        <input type="text"  v-model="dbv.estado"  name="estado" id="estado">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="classe">Classes</label>
                        <input type="text"  v-model="dbv.classe"  name="classe" id="classe">
                        </div>
                    </div>
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="unidade">Unidades</label>
                        <input type="text"  v-model="dbv.unidade"  name="unidade" id="unidade">
                        </div>
                    </div> -->
                    <div class="col-12">
                        <div class="form_conteiner">
                        <label for="imagem">Imagem</label>
                        <input type="text"  v-model="dbv.img"  name="imagem" id="imagem">
                        </div>
                    </div>            
                    <div class="col-12">
                        <div class="c_rodape_form">
                        <button type="submit" v-if="!btn_editar" v-on:click="addDbv" >Cadastrar</button>
                        <button type="submit" v-if="btn_editar"  v-on:click="editarDbv" >Editar</button>                
                        <button class="voltar" type="button" v-on:click="voltar">Voltar</button>
                        </div>
                    </div>                                                                                                
                </div>
        </div>

    </div>
</template>
<script>
import Paginate from 'vuejs-paginate';
export default {
 name:"App",
 data(){
     return {
         dbv:{
             id:'',
             nome:'',
             idade:'',
             sexo:'',
             img:require('@/assets/face4.jpg'),
             endereco:'',
             complemento:'',
             numero:'',                          
             bairro:'',                          
             cidade:'',                          
             estado:'',
             unidade:'',
             classe:''                          
         },
         dbvs:[],
         lista_dbvs:[],
         unidade:[{
             unidade:'',
             id_unidade:''
         }],
         classe_dbv:[{
             classe_dbv_nome:'',
             id_classe_dbv_nome:''
         }],
         ocultar:false,
         btn_editar:false,
         campo_pesquisa:'',
         paginas_a_ser_paginadas:0,
         pagina_atual:0
     }
 },
 methods: {
     addDbv(){
         console.log('data: ',this.dbv);
            const formularioData = Object.assign({},this.dbv); 
                this.dbvs.push(formularioData);
                this.db_add(formularioData);
                //limpar formulario
                 this.dbv.nome = '';
                    this.ocultarDiv();
     },
     excluirDbv(index){
            this.dbvs.splice(index,1);
     },
     editarFormDbv(registro,index){
            this.btn_editar = !this.btn_editar;
            this.dbv = registro;
            this.ocultarDiv();
     },
     editarDbv(registro,index){
         this.btn_editar = !this.btn_editar;
            this.dbv = registro;
                this.dbvs[index]=registro;    
                    this.ocultarDiv();
     },     
     pesquisarDbv(){
         if(this.campo_pesquisa !== ''){
             const dados = this.dbvs.filter(el=>el.nome.includes(this.campo_pesquisa));
                this.dbvs = dados;
                    return;
         }
        this.dbvs = this.recarregar_tela();
     },
     recarregar_tela(){
        const c = this.db_listar();
            if(c.length > 0){
                return JSON.parse(c);
            }else{
                return [];
            }
     },
     ocultarDiv(){
         this.$el.querySelector('.conteiner_central').classList.toggle('ocultar_conteudo');
        //  this.$el.querySelector('.lista_desbravadores_conteiner').classList.toggle('ocultar_conteudo');
     },
     voltar(){
         this.ocultarDiv();
     },
     funcao_paaginacao(numPage){
         console.log('fnção de click da paginação:',numPage);
         this.pagina_atual = (numPage -1);
     },
     db_add(data){
            let db = this.db_listar();
                if(db.length > 0){
                    db = JSON.parse(db);
                    db.push(data);
                }else{
                    db =[];
                    db.push(data);
                }
                    localStorage.setItem("dbv_data",JSON.stringify(db));
        },
        db_editar(data,index){
                let db = this.db_listar();
                    if(db.length > 0){
                        db = JSON.parse(db);
                            db[index]=data;
                                localStorage.setItem("dbv_data",JSON.stringify(db));                    
                    }
        },
        db_excluir(index){
            let db = this.db_listar();
                if(db.length > 0){
                    db = JSON.parse(db);
                         db.splice(index,1);
                            localStorage.setItem("dbv_data",JSON.stringify(db));                    
                }
        },        
        db_listar(){
             if(localStorage.getItem("dbv_data")){
                 return localStorage.getItem("dbv_data");
             }else{
                 localStorage.setItem("dbv_data","");
                 return localStorage.getItem("dbv_data");
             }
        },        
        db_pesquisa(){
            let db = this.db_listar();
                if(db.length > 0){
                    db = JSON.parse(db);
                        console.log('dados psquisado',db.filter(el=>el.nome.includes(this.campo_pesquisa)));
                }
             
        },        
     /*fim funcoes de baco de dados*/ 
     /*paginacao funcao auxiliar*/
        paginacao_auxiliar(arr,total_registros,itens_por_pagina){
            let separados = [];
            for(var i=0;i<total_registros;i+=itens_por_pagina){
                separados.push(arr.slice(i,i+itens_por_pagina))
            }
            return separados
        }
 },
 components:{
     Paginate
 },
 beforeMount(){ 
     const c = this.db_listar();
        if(c.length > 0){
            const db = JSON.parse(c);
            this.dbvs = db;
        }else{
            const db =[];
            this.dbvs=db;            
        }
    //paginacao
        let paginas = Math.round(this.dbvs.length/2);
            console.log('resultado matematico ',paginas);
                this.paginas_a_ser_paginadas = paginas;
    //subdividindo a array geral
            const itens_por_pagina =2;
            const total_registros = this.dbvs.length;
            let separados = [];
            
                for(var i=0;i<total_registros;i+=itens_por_pagina){
                    separados.push(this.dbvs.slice(i,i+itens_por_pagina))
                }           
                    this.lista_dbvs = separados;
                        console.log('a lista a ser exibida e ',this.lista_dbvs);
 }
}
</script>
<style lang="css" >
*{
    margin:0;
    padding:0;
    box-sizing: margin-box;
}
.conteiner-principal{
    position: relative;
}
.conteiner-principal > .row{
    position: absolute;
    top: 10px;
    left: auto;

}
.lista_desbravadores_conteiner {
    transform: translateX(32vw);
}
.conteiner_central
{
    background-color: #fff;
    width: 100vw;
    height: 100vh;
    margin: 10px auto;
    transition: .3s;
    transform: translateX(0vw);
}

.form_conteiner{
    display: flex;
    flex-direction: column;
    padding: 1.5rem;
}
.form_conteiner input
{
    padding: 14px 35px;
    border-radius: 0.5em;
    outline: none;
    font-size: 1.5em;
    border: 1px solid #d6d6d6;
    color: #4a4a4a;
}
.form_conteiner label
{
    padding: 10px 34px;
    font-size: 1.5em;
    font-family: sans-serif;
    color: #3c3c3c;
}

.c_rodape_form{
    display: grid;
    grid-template-columns: repeat(2,1fr);
}
button{
    padding: 1.2rem;
    border: 0;
    background: #122bdb;
    color: #fff;
    font-size: 1.3em;
    cursor: pointer;
}
.voltar{
    padding: 1.2rem;
    border: 0;
    background: #dbb612;
    color: #fff;
    font-size: 1.3em;
    cursor: pointer;
}

.pesquisaBox{
    display: flex;
    margin: 0.2rem
}
.cabecalho{
    width: 35vw;
    border: 1px solid #c9c9c9;
    margin: 1vw auto;
    display: flex;
    justify-content: space-between;
}
.cabecalho input{
    width: 13rem;
    margin-left: 0.5rem;
    padding: 1em;
    font-size: 1.3rem;
}

.tabela{
    margin: 0 auto;
    border: 0px solid #000;
    display: grid;
    justify-content: center;
    width: 35vw;
}
.tabela .linha{
    display: grid;
    grid-template-columns: repeat(4,1fr);
    margin-bottom: .4rem;
    gap:.1rem;
}
.col-1{
    padding: 1rem;
    text-align: center;
    border: 1px solid #afafaf;
       
}
.ocultar_conteudo{
    transform: translateX(100vw);
}

.item_paginacao
{
    border: 1px solid #9f9f9f !important;
    list-style: none !important;
    padding: 1em !important;    
}

.ul_paginacao{
    background: #ffffff;
    display: flex;
    border:1px solid #ff000000;
    width: 25vw;
    justify-content: space-around;
    margin: 0 auto;
    list-style: none;
    padding:1em;

}
.page-item {
    padding: 1em !important;
    transition: .5s;
    transform-origin: top;
}

.page-item.active {
    background-color: #4613d6 !important;
    padding: 1em !important;
    color: #fff !important;
}
</style>