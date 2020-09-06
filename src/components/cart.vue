<!--Componente para todo tipo de productos-->
<template>
	<div>
		<div class="d-flex mb-2" v-for="producto in datosCarrito">
			<img :src="producto.producto.imagen" class="m-1"></img>
			<h4 class="m-1">{{producto.producto.titulo}}</h4>
			<!--<input class="m-1 form-control w-25" type="number" v-model="producto.cantidad" min="1" @change="cambiarCantidad()">-->
			<div class="input-group mb-3 w-25">
			  	<div class="input-group-prepend">
			    	<span class="input-group-text" v-on:click="producto.cantidad--, cambiarCantidad()"><i class="fas fa-minus"></i></span>
			  	</div>
			  	<input class="form-control" type="number" v-model="producto.cantidad" min="1" @change="cambiarCantidad()">
			  	<div class="input-group-append">
			    	<span class="input-group-text"v-on:click="producto.cantidad++, cambiarCantidad()"><i class="fas fa-plus"></i></span>
			  	</div>
			</div>
            <h3 class="m-1">${{producto.cantidad > 0 ? producto.producto.precio * producto.cantidad : 0}}</h3>
		</div>

		<div>
			<h3 class="float-left">TOTAL: ${{total()}}</h3>
			<button class="btn btn-success float-right" v-on:click="pagar()">PAGAR</button>
		</div>
	</div>
</template>

<script>

	export default {
		name: "carro",
		//Titulo del producto, despricion y el precio por ejemplo 52000
		//Link de la imagen
		data() {
			return {
				datosCarrito: JSON.parse(localStorage.getItem("Carrito")),
				precioTotal: 0,
			}
		},
		components: {
		},
		methods: {
			//Envia el pedido al back end
			pagar: function () {
				const axios = require('axios');

				axios.post('http://localhost:3000/datos', this.datosCarrito)
				  .then(function (response) {
				    console.log(response);
				  });

				  this.datosCarrito = [];
				  localStorage.setItem('Carrito', JSON.stringify(this.datosCarrito));
			},

			//Cambia la cantidad de elementos
			cambiarCantidad: function() {
				if (typeof(Storage) !== "undefined") {
				    localStorage.setItem('Carrito', JSON.stringify(this.datosCarrito));
				}
				this.total();
			},
			//Calcula el total de la compra
			total: function () {
				this.precioTotal = 0;
				this.datosCarrito.forEach(value => {
					this.precioTotal += value.cantidad * value.producto.precio;
				})
				return this.precioTotal;
			}
		}
	}


</script>

<style lang="scss">
  @import "../styles/custom.scss";
  @import '../../node_modules/bootstrap/scss/bootstrap.scss';

  .d-flex {
  	display: flex;
    align-items: center;

  	img {
	  	width: auto;
	  	height: 30px;
  	}
  }
</style>