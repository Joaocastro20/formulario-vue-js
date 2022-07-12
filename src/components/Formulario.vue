<template>
<div class="container">
    <div class="cabecalhoform">
      <h5 class="texto">Formularios <br>para compra de <br><strong>Pacotes de Adesivos</strong> </h5>
    </div>
    <div class="corpoform">
      <h5 class="texto">Selecione os adesivos e suas quantidades:</h5>
      <table class="texto">
        <tr>
          <td><label for="scales">React</label></td>
          <td>
            <label for="scales"> 
            <div class="texto">
            <button v-on:click="remReactCem">-100</button>
            <button v-on:click="remReact">-1</button>
            <input type="text" disabled v-model="react">
            <button v-on:click="addReact">+1</button>
            <button v-on:click="addReactCem">+100</button>
            </div></label>
            </td>
        </tr>
        <tr>
          <td><label for="scales">Vue js</label></td>
          <td>
            <div class="texto">
            <button v-on:click="remVueCem">-100</button>
            <button v-on:click="remVue">-1</button>
            <input type="text" disabled v-model="vue">
            <button v-on:click="addVue">+1</button>
            <button v-on:click="addVueCem">+100</button>
            </div>
          </td>
        </tr>
        <tr>
          <td><label for="scales">Angular</label></td>
          <td>
          <div class="texto">
            <button v-on:click="remAngularCem">-100</button>
            <button v-on:click="remAngular">-1</button>
            <input type="number" disabled v-model="angular">
            <button v-on:click="addAngular">+1</button>
            <button v-on:click="addAngularCem">+100</button>
          </div>
          </td>
        </tr>
      </table>
      
      </div>
      <div class="texto">
      <h6>Observações:</h6>
      <input class="input-texto"  type="text" maxlength="22" v-model="valorobservacao">
      </div>
      <div v-if="pedido.situacao != true" class="rodapeform"><button class="btn btn-primary" v-on:click="salvarPedido">Continuar</button>
      </div>
   
    <div class="checkout"  v-if="pedido.situacao != false">
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
          react:Number = 0,
          vue:Number = 0,
          angular:Number = 0,
          

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
          this.pedido.reactqtd = this.react
          this.pedido.vueqtd = this.vue
          this.pedido.angularqtd = this.angular
          this.pedido.observacao = this.valorobservacao
          this.pedido.situacao = true
          console.log(this.pedido)
        },

        confirmarPedido(){
          alert('pedido realizado')
        },
        voltarPedido(){
          this.pedido.situacao = false
        },
        addReact(){
          this.react++
        },
        addReactCem(){
          this.react = this.react + 100
        },
        remReact(){
          if(this.react <= 0){
            this.react = 0
          }else{
            this.react--
          }
        },
        remReactCem(){
          if(this.react <= 100){
            this.react = 0
          }else{
            this.react = this.react -100
          }
        },

        addVue(){
          this.vue++
        },
        addVueCem(){
          this.vue = this.vue + 100
        },
        remVue(){
          if(this.vue <= 0){
            this.vue = 0
          }else{
            this.vue--
          }
        },
        remVueCem(){
          if(this.vue <= 100){
            this.vue = 0
          }else{
            this.vue = this.vue - 100
          }
        },

        addAngular(){
          this.angular++
        },
        addAngularCem(){
          this.angular = this.angular + 100
        },
        remAngular(){
          if(this.angular <= 0){
            this.angular = 0
          }else{
            this.angular--
          }
        },
        remAngularCem(){
          if(this.angular <= 100){
            this.angular = 0
          }else{
            this.angular = this.angular - 100
          }
        }

    }
}
</script>
<style>
.container{
  background-color: rgb(255, 255, 255);
   margin-top: 10px;
   width: 900px;
   text-align: center;
   border-radius: 10px 10px;
   box-shadow: 10px 5px 5px rgba(0, 0, 0, 0.247);
   padding: 0%;
   text-align: justify;
   
}
.cabecalhoform{
  height: 200px;
  border-bottom-left-radius:30%;
      border-bottom-right-radius:70%;
      background-color: rgba(28, 5, 131, 0.877);
  color: aliceblue;
}
.rodapeform{
  background-color: rgba(128, 128, 128, 0.493);
  border-radius: 10px;
  text-align: center;

  
}
.corpoform{
  height: 150px;
}
.checkout{
  margin-top: 10px;
  background-color: rgba(128, 128, 128, 0.493);
}
.texto{
  margin: 5px 30px 0px 30px;
  font-weight: 300;
}
.input-texto{
  margin: 5px 30px 10px 30px;
  height: 100px;
  width: 300px;
  text-align:start;
}
.observacoes{
  display: block;
    margin: 0 auto;
}

</style>
