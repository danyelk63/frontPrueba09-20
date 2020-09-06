<!--Componente para todo tipo de productos-->
<template>
	<div class="col-md-10 row mx-auto">
		<div class="m-3 p-3 col-md-2 padre" v-for="producto in productos">
		    <img :src="producto.imagen"></img>
		    <h4 class="text-center">{{producto.titulo}}</h4>
		    <p class="text-center">{{producto.descripcion}}</p>
		    <div class="elementosPA">
			    <h5 class="text-center">Precio: ${{producto.precio}}</h5>
			    <button class="btn btn-primary mx-auto d-block mx-auto" v-on:click="agregarProducto(producto)">Añadir al carrito</button>
		    </div>
		</div>
	</div>
</template>

<script>
	export default {
		name: "producto",
		//Titulo del producto, despricion y el precio por ejemplo 52000
		//Link de la imagen
		props: ['productos'],
		data() {
			return {
				itemCount: 0
			}
		},
		components: {
		},
		data() {
			return {
				listaCarrito: []
			}
		},
		methods: {
			//Esta funcion añade los nuevos elementos al carrito y lo guarda en el local storage
			agregarProducto: function (p) {
				var bandera = false;

				if (typeof(Storage) !== "undefined") {
				    this.listaCarrito = JSON.parse(localStorage.getItem("Carrito"))
				    if (this.listaCarrito == null)
				    	this.listaCarrito = [];
				} 

				this.listaCarrito.forEach(value => {
					if(value.producto == p){
						value.cantidad++;
						bandera = true;
					}
				})

				if(this.listaCarrito.length == 0 || !bandera){
					this.listaCarrito.push({producto: p, cantidad: 1});
				}
				
				if (typeof(Storage) !== "undefined") {
				    localStorage.setItem('Carrito', JSON.stringify(this.listaCarrito));
				} 
			}
		}
	}

	
</script>

<style lang="scss">
  @import "../styles/custom.scss";
  @import '../../node_modules/bootstrap/scss/bootstrap.scss';
  
  .padre {
  	position: relative;
  	height: 75vh;
    img {
      width: 100%;
    }

    .elementosPA {
    	margin-top: 100vh;
    	position: absolute;
    	bottom: 0;
    	display: block;
    }
  }
</style>