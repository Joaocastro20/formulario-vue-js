<template>
<div class="container">
    <h5>Formularios para compra de Pacotes de Adesivos</h5>
    <h6>Quais Adesivos:</h6>
    <div>
      <label for="scales">React</label>
      <input type="number" min="0" max="4000" v-model="valorreact">
    </div>
    <div>
      <label for="scales">Vue</label>
      <input type="number" min="0" max="4000" v-model="valorvue">
    </div>
    <div>
      <label for="scales">Angular</label>
      <input type="number" min="0" max="4000" v-model="valorangular">
    </div>
    <h6>Observações:</h6>
    <input type="text" maxlength="22" v-model="valorobservacao">
    <div><button v-on:click="salvarPedido">Enviar</button></div>
    <div  v-if="pedido.situacao != false">
    <div>
      <h5>Verifique seu pedido:</h5>
      <p>React:{{pedido.reactqtd}}</p>
      <p>Vue:{{pedido.vueqtd}}</p>
      <p>Angular:{{pedido.angularqtd}}</p>
    </div>
    <div>
      <button v-on:click="confirmarPedido">confirmar</button>
      <button v-on:click="voltarPedido">voltar</button>
    </div>
      
    </div>
</div>

</template>
<script>

export default{
    data(){
        
        return{
          
          pedido:{
          reactqtd:Number,
          vueqtd:Number,
          angularqtd:Number,
          observacao:String,
          situacao:Boolean = false
          }}
          
        
    },
    methods:{
        salvarPedido(){
          this.pedido.reactqtd = this.valorreact
          this.pedido.vueqtd = this.valorvue
          this.pedido.angularqtd = this.valorangular
          this.pedido.observacao = this.valorobservacao
          this.pedido.situacao = true
        },

        confirmarPedido(){
          alert('pedido realizado')
        },
        voltarPedido(){
          this.pedido.situacao = false
        },
    }
}
</script>

