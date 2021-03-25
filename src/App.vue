<template>
  <div id="app">
    <h1>PIX</h1>

    <div class="input-container">
      <div class="input-form">
        <input type="text" v-model="key" id="key" required>
        <label for="key">Chave PIX</label>
      </div>
    </div>

    <div class="input-container">
      <div class="input-form">
        <input type="text" v-model="name" id="name" required>
        <label for="name">Nome</label>
      </div>
    </div>

    <div class="input-container">
      <div class="input-form">
        <input type="text" v-model="city" id="city" required>
        <label for="city">Cidade</label>
      </div>
    </div>

    <div class="input-container">
      <div class="input-form">
        <input type="text" v-model="message" id="message" required>
        <label for="message">Mensagem</label>
      </div>
    </div>

    <div class="input-container">
      <div class="input-form">
        <input type="text" v-model="cep" id="cep" required>
        <label for="cep">CEP</label>
      </div>
    </div>

    <div class="input-container">
      <div class="input-form">
        <input type="text" v-model="amount" id="amount" required>
        <label for="amount">Quantidade em R$</label>
      </div>
    </div>

    <button @click="generate()" class="btn">Gerar QR Code</button>

    <div v-if="amount > 0">
      <img alt="" :src="image">
    </div>
  </div>
</template>

<script>
import { QrCodePix } from 'qrcode-pix'

export default {
  name: 'App',

  data() {
    return {
      image: '',
      key: '00000000000',
      name: 'Jardel Frank',
      city: 'Caicó',
      message: 'Pagamento',
      cep: '59300000',
      amount: 0.0
    }
  },

  methods: {
    generate() {
      const qrCodePix = QrCodePix({
        version: '01',
        key: this.key, //or any PIX key
        name: this.name,
        city: this.city,
        guid: 'YOUR_GUID',
        message: this.message,
        cep: this.cep,
        value: Number(this.amount),
      })
      
      console.log(qrCodePix.payload()) // '00020101021126510014BR.GOV.BCB.PIX...'
      console.log(qrCodePix.base64()) // 'data:image/png;base64,iVBORw0...'
      
      Promise.resolve(qrCodePix.base64()).then(value => {
        this.image = value
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

/**
 * @inputs
 */
.select {
	position: relative;
	width: 100%;
	height: 35px;
	margin-top:10px;
	margin-bottom:5px;
}

.select-text {
	position: relative;
	width: 100%;
	height: 35px;
	background-color: transparent;
	padding-top: 5px;
	font-size: 18px;
	border-radius: 0;
	border: none;
}

.select-label {
	color: #B0BEC5;
	font-size: 18px;
	position: absolute;
	pointer-events: none;
	left: 0;
	top: 10px;
	transition: 0.2s ease all;
}

/* active state */
.select-text:focus ~ .select-label, .select-text:valid ~ .select-label {
	top: -10px;
	transition: 0.2s;
	font-size: 14px;
}
.select-text:focus ~ .select-label {
	color: dodgerblue;
}

/* BOTTOM BARS ================================= */
.select-bar {
	position: relative;
	display: block;
	width: 100%;
	border-bottom: 2px solid #B0BEC5;
	transition: .2s;
}

/* active state */
.select-text:focus ~ .select-bar {
	border-bottom: 2px solid dodgerblue;
}


.input-legend {
	right: 25px;
	position: absolute;
	cursor: pointer;
	margin-top: 8px;
}


input {
	font-size:12pt;
	font-weight: bold;
}

.input-container {
	display: block;
	padding-top: 15px;
	padding-bottom: 15px;
}

.input-form {
	width: 100%;
	position: relative;
}

.input-form input,
.input-form textarea {
	width: 100%;
	height: 30px;

	font-weight: normal;

	box-shadow: 0 0 0 0;
	outline: 0;
	border:none;
	border-bottom:2px solid #CFD8DC;

	transition: .2s ease all;

	background: transparent;
}

.input-form label {
	position: absolute;
	top: 5px;
	left: 0;
	right: 0;

	color: #B0BEC5;

	display: flex;
	align-items: center;

	cursor: text;
	transition: .2s ease all;
	box-sizing: border-box;
}


.input-form input:focus,
.input-form textarea:focus {
	border-bottom: 2px solid dodgerblue;
}

input:valid + label,
textarea:valid + label {
	font-size: 10pt;
	top: -13px;
	pointer-events: none;
}

.input-form input:focus + label,
.input-form textarea:focus + label {
	color: dodgerblue;
	font-size: 10pt;
	top: -13px;
	pointer-events: none;
}

input:focus,
input:-webkit-autofill {
	background: transparent;
	-webkit-box-shadow: 0 0 0 30px transparent inset;
	outline: 0;
}


/**button */
.btn {
	min-width:100px;
	height: 40px;
	border-radius:5px;
	border:none;
	padding:4px 10px 4px 10px;
	font-weight: bold;
	cursor: pointer;
	transition: .3s;
	outline: none;
	background: dodgerblue;
	color:white;
}
.btn:hover {
	background: rgb(3, 91, 179);
}
</style>
