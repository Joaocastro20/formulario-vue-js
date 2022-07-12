<template>
  <div class="container">
    <div class="cabecalhoform">
      <h5 class="texto">Formularios <br>para compra de <br><strong>Pacotes de Adesivos</strong> </h5>
    </div>
    <div v-if="pedido.situacao != true" class="corpoform">
      <h5 class="texto">Selecione os adesivos e suas quantidades:</h5>
      <table class="texto">
        <tr>
          <td><label for="scales">React</label></td>
          <td>
            <label for="scales">
              <div class="texto">
                <button class="botao" v-on:click="remReactCem">-100</button>
                <button class="botao" v-on:click="remReact">-1</button>
                <input type="text" disabled v-model="react">
                <button class="botao" v-on:click="addReact">+1</button>
                <button class="botao" v-on:click="addReactCem">+100</button>
              </div>
            </label>
          </td>
        </tr>
        <tr>
          <td><label for="scales">Vue js</label></td>
          <td>
            <div class="texto">
              <button class="botao" v-on:click="remVueCem">-100</button>
              <button class="botao" v-on:click="remVue">-1</button>
              <input type="text" disabled v-model="vue">
              <button class="botao" v-on:click="addVue">+1</button>
              <button class="botao" v-on:click="addVueCem">+100</button>
            </div>
          </td>
        </tr>
        <tr>
          <td><label for="scales">Angular</label></td>
          <td>
            <div class="texto">
              <button class="botao" v-on:click="remAngularCem">-100</button>
              <button class="botao" v-on:click="remAngular">-1</button>
              <input type="number" disabled v-model="angular">
              <button class="botao" v-on:click="addAngular">+1</button>
              <button class="botao" v-on:click="addAngularCem">+100</button>
            </div>
          </td>
        </tr>
      </table>

    </div>
    <div v-if="pedido.situacao != true" class="texto">
      <h6>Observações:</h6>
      <input class="input-texto" placeholder="Duvidas? Recados?" type="text" maxlength="500" v-model="valorobservacao">
    </div>
    <div v-if="pedido.situacao != true" class="rodapeform"><button class="botao"
        v-on:click="salvarPedido">Continuar</button>
    </div>

    <div class="checkout" v-if="pedido.situacao != false">
      <div class="texto">
        <h5>Verifique seu pedido:</h5>
        <p>React:{{ pedido.reactqtd }}</p>
        <p>Vue:{{ pedido.vueqtd }}</p>
        <p>Angular:{{ pedido.angularqtd }}</p>
        <p>Total de Adesivos:{{ totaladesivos }}</p>
        <p>Total R$:{{ totalapagar }}</p>
      </div>
      <div class="texto">
        <h5>Cupom de Desconto:</h5>
        <input v-model="cupom" placeholder="BEMPAGGO" type="text">
        <button class="botao" v-on:click="aplicarCupom">Aplicar Cupom</button>
      </div>
      <div class="texto">
        <label for="cars"><strong>Selecione a Forma de Pagamento:</strong></label>
        <select name="formapagamento" id="formapagamento">
          <option value="cartaodecredito">Cartão de Crédito</option>
          <option value="boleto">Boleto</option>
          <option value="pix">Pix</option>
        </select>
      </div>
      <div class="texto" v-if="formapagamento == cartaodecredito">
        <div>
          <h5>
            Informações Para Pagamento:
          </h5>
        </div>
        <p>
          <input type="text" placeholder="Your name" autofocus>
          <input type="text" placeholder="MM">
          <input type="text" placeholder="YY">
        </p>
        <p>
          <input type="text" placeholder="4111 1111 1111 1111">
          <input type="text" placeholder="CVC">
        </p>
        <p>
          <button value="checkout" class="botao">Checkout</button>
        </p>
      </div>
      <div class="rodapeform">
        <button class="botao" v-on:click="voltarPedido">voltar</button>
        <button class="botao" v-on:click="confirmarPedido">confirmar</button>
      </div>/?
    </div>
  </div>

</template>
<script>



export default {
  data() {

    return {
      react: Number = 0,
      vue: Number = 0,
      angular: Number = 0,
      totaladesivos: Number,
      totalapagar: Number,
      valoradesivo: Number = 0.50,
      validarcupom: Boolean = true,



      pedido: {
        reactqtd: Number,
        vueqtd: Number,
        angularqtd: Number,
        observacao: String,
        situacao: Boolean = false
        ,

        totalAdesivos() {
          return this.reactqtd + this.vueqtd + this.angularqtd
        }
      }
    }


  },
  methods: {
    salvarPedido() {
      this.pedido.reactqtd = this.react
      this.pedido.vueqtd = this.vue
      this.pedido.angularqtd = this.angular
      this.pedido.observacao = this.valorobservacao
      this.pedido.situacao = true
      this.totaladesivos = this.pedido.totalAdesivos()
      this.totalapagar = this.pedido.totalAdesivos() * this.valoradesivo
      console.log(this.pedido)
    },
    aplicarCupom() {
      if (this.cupom == 'BEMPAGGO' && this.validarcupom == true) {
        this.totalapagar = this.totalapagar - (this.totalapagar * 0.15)
        this.validarcupom = false
      }

    },

    confirmarPedido() {
      alert('pedido realizado')
    },
    voltarPedido() {
      this.pedido.situacao = false
      this.validarcupom = true

    },
    addReact() {
      this.react++
    },
    addReactCem() {
      this.react = this.react + 100
    },
    remReact() {
      if (this.react <= 0) {
        this.react = 0
      } else {
        this.react--
      }
    },
    remReactCem() {
      if (this.react <= 100) {
        this.react = 0
      } else {
        this.react = this.react - 100
      }
    },

    addVue() {
      this.vue++
    },
    addVueCem() {
      this.vue = this.vue + 100
    },
    remVue() {
      if (this.vue <= 0) {
        this.vue = 0
      } else {
        this.vue--
      }
    },
    remVueCem() {
      if (this.vue <= 100) {
        this.vue = 0
      } else {
        this.vue = this.vue - 100
      }
    },

    addAngular() {
      this.angular++
    },
    addAngularCem() {
      this.angular = this.angular + 100
    },
    remAngular() {
      if (this.angular <= 0) {
        this.angular = 0
      } else {
        this.angular--
      }
    },
    remAngularCem() {
      if (this.angular <= 100) {
        this.angular = 0
      } else {
        this.angular = this.angular - 100
      }
    }

  }
}
</script>
<style>
.container {
  background-color: rgb(255, 255, 255);
  margin-top: 10px;
  width: 900px;
  text-align: center;
  border-radius: 10px 10px;
  box-shadow: 10px 5px 5px rgba(0, 0, 0, 0.247);
  padding: 0%;
  text-align: justify;

}

.cabecalhoform {
  height: 200px;
  border-bottom-left-radius: 30%;
  border-bottom-right-radius: 70%;
  background-color: rgba(28, 5, 131, 0.877);
  color: aliceblue;
}

.rodapeform {
  background-color: rgba(128, 128, 128, 0.493);
  border-radius: 10px;
  text-align: center;
}

.botao {
  background-color: rgba(28, 5, 131, 0.877);
  color: white;
  border-radius: 20px;
}

.corpoform {
  height: 150px;
}

.checkout {
  margin-top: 10px;
}

.texto {
  margin: 5px 30px 0px 30px;
  font-weight: 300;
}

.input-texto {
  margin: 5px 30px 10px 30px;
  height: 100px;
  border-radius: 10px;
  width: 300px;
  text-align: start;
  background-color: rgba(187, 187, 187, 0.822);
}

.observacoes {
  display: block;
  margin: 0 auto;
}
</style>
