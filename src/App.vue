<template>
  <div id="app">
    
    <h3>Cadastro:</h3>
    
    <input type="text" placeholder="nome" v-model="nomeField"><br>
    <input type="email" placeholder="email" v-model="emailField"><br>
    <input type="number" placeholder="idade" v-model="idadeField"><br>
    <button @click=" cadastrarUsuario ">Cadastrar</button>
    <small id="nomeErro" v-show="deuErro"> Cadastro invalido</small><br>
    <hr>
      
      <div v-for="(TestCliente, index) in clientes" :key='TestCliente.id'>
        <h4>{{ index+ 1 }}</h4>
        <TestCliente :cliente="TestCliente" @meDelete="deletarUsuario($event)"/>
       
        
      </div>

  </div>
</template>

<script>

import TestCliente from './components/TestCliente.vue'
//import ProdutoUm from './components/ProdutoUm.vue'
export default {
  name: 'App',
  data(){
    return{
      deuErro: false,
      
      nomeField:"",
      emailField:"",
      idadeField:0,


      clientes: [
        {
          id: 2,
          nome: "Victor Lima",
        email:"victor@lima.com",
        idade: 60
        },
        {
          id: 3,
          nome: "Michael Scott",
        email:"michael@lima.com",
        idade: 60
        },
        {
          id: 4,
          nome: "Ednaldo Pereira",
        email:"edinaldo.prereira@lima.com",
        idade: 60
        },
        {
          id: 5,
          nome: "Ricardo Milos",
        email:"milos.ricardo@lima.com",
        idade: 60
        },
      ] 
    }
  },

  components: {
   TestCliente,
   // ProdutoUm
  },
  methods:{
    cadastrarUsuario: function(){
      if( this.nomeField =="" || this.emailField == "" || this.nomeField.length < 3){
        this.deuErro = true
      }
      else{

        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now})
        this.nomeField = "",
        this.emailField = "",
        this.idadeField = "",
        this.deuErro = false
      }
    },
    deletarUsuario: function($event){
      var id = $event.idDoCliente;
      var novoArray = this.clientes.filter(TestCliente=> TestCliente.id != id);
      this.clientes = novoArray;
      
    }
  }
}
</script>

<style>

  #nomeErro{
    color: red;
  }


</style>
