<template>
    <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
        <h4>Nome: {{ cliente.nome }} </h4>
        <hr>
        <p>Email: {{cliente.email | processarEmail}}</p>
        <p v-if="showIdade === true">Idade: {{cliente.idade}}</p>
        <p v-else>O usuário escondeu a idade!</p>
        <button @click="mudarCor">Mudar cor!</button>
        <button @click="emitirEventoDelete">Deletar</button>
        <h4>Id especial: {{idEspecial}}</h4>
                

    </div>
</template>

<script>
export default {
    data(){
        return{
            isPremium: false,
            
            
            
            
        }

    },
    props:{
        cliente: Object,
        showIdade: Boolean,
    },
    methods:{
        mudarCor: function(){
            this.isPremium= !this.isPremium;
        },
        emitirEventoDelete: function(){
            
            this.$emit("meDelete", {idDoCliente: this.cliente.id,component: this});
            
        },
        testar: function(){
            console.log("Testando rpa valer!");
            alert("isso é um alert!");
        },
        
    },
    filters:{
            processarEmail: function(value){
                return value.toUpperCase();
            }
        },

    computed:{
        idEspecial: function(){
            return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
    }
}
</script>

<style scoped>
    .cliente{
        background-color: #ECE5E3;
        max-width: 600px;
        height: 180px;
        padding: 1%;
        margin-top: 2%;
    }

    .cliente-premium{
        background-color: black;
        color: gold;
        max-width: 600px;
        height: 180px;
        padding: 1%;
        margin-top: 2%;
    }



</style>