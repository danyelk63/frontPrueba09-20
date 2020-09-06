<template>
  <div class="m-5">
    <div class="d-flex">
    <img class="mx-auto" src="https://cdn.worldvectorlogo.com/logos/citizen-2.svg">
    <div class="iconoCarrito" v-on:click="mostrarCarro(true)">
      <i class="fas fa-shopping-cart fa-3x"></i>
      <div class="puntito" id="puntito"></div>
    </div>
  </div>

  <!--Vista de los productos-->
  <div>
  <div id="fondo"></div>
    <producto v-bind:productos="listaProd"></producto>
  </div>

  <!--Vista carrito-->
  <div class="carro p-4 border" id="carro">
    <i class="cruz far fa-times-circle fa-3x" v-on:click="mostrarCarro(false)"></i>
    <carro v-if="mostrarCarroBool"></carro>
  </div>
  </div>

</template>

<script>
  import Producto from './components/product';
  import Carro from './components/cart';

  export default {
    name: 'app',
    components: {
      Producto,
      Carro
    },
    data() {
      return {
        listaProd: [
          {imagen: "https://www.kevins.com.co/img/productos/4974374265104.jpg", titulo: "REF. 4974374265104", descripcion: "Reloj citizen analogo, para hombre, tablero redondo colores gris y rosa, estilo index + romano, pulso acero color plateado , Diámetro: 38.50mm , Resistencia al agua: 10 bares", precio: "5705000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374284280.jpg", titulo: "REF. 4974374284280", descripcion: "Reloj citizen analogo, para dama, tablero redondo colores transparente, dorado y beige, estilo index, pulso acero color dorado , Diámetro: 27.00mm , Resistencia al agua: 5 bares", precio: "1019000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374247520.jpg", titulo: "REF. 4974374247520", descripcion: "Reloj citizen analogo, para hombre, tablero redondo colores negro y plateado, estilo index, pulso metalico color plateado, calendario , Diámetro: 41.00mm , Resistencia al agua: 5 bares", precio: "299000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374264237.jpg", titulo: "REF. 4974374264237", descripcion: "Reloj citizen analogo, para hombre, tablero redondo colores negro y rosa, estilo puntos, pulso silicona color negro, calendario , Diámetro: 46.00mm , Resistencia al agua: 10 bares", precio: "637000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374265081.jpg", titulo: "REF. 4974374265081", descripcion: "Reloj citizen analogo, para hombre, tablero redondo color negro, estilo index, pulso metalico color plateado , Diámetro: 38.50mm , Resistencia al agua: 3 bares", precio: "4992000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374263711.jpg", titulo: "REF. 4974374263711", descripcion: "Reloj citizen analogo, para hombre, tablero redondo colores plateado, dorado y negro, estilo romanos, pulso acero color plateado, calendario , Diámetro: 41.00mm , Resistencia al agua: 5 bares", precio: "573000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374286864.jpg", titulo: "REF. 4974374286864", descripcion: "Reloj citizen analogo, para hombre, tablero redondo colores negro y plateado, estilo index, pulso acero color negro , Diámetro: 39.00mm , Resistencia al agua: 5 bares", precio: "416000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374261625.jpg", titulo: "REF. 4974374261625", descripcion: "Reloj citizen analogo, para hombre, tablero redondo colores negro y blanco, estilo index + arabigo, pulso acero color plateado, calendario , Diámetro: 40.00mm , Resistencia al agua: 5 bares", precio: "308000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374275257.jpg", titulo: "REF. 4974374275257", descripcion: "Reloj citizen analogo, para hombre, tablero redondo color gris, estilo index, pulso metalico color plateado, calendario , Diámetro: 40.50mm , Resistencia al agua: 5 bares", precio: "364000"},
          {imagen: "https://www.kevins.com.co/img/productos/4974374275363.jpg", titulo: "REF. 4974374275363", descripcion: "Reloj citizen analogo, para dama, tablero redondo colores dorado y negro, estilo arabigos, pulso metalico color dorado, calendario , Diámetro: 26.00mm , Resistencia al agua: 5 bares", precio: "355000"}
        ],
        mostrarCarroBool: false
      }
    },
    methods: {
      //Activa y desactiva el modal del carro de compras
      mostrarCarro: function (opcion) {
        if(opcion && carritoCompleto != null){
          document.getElementById("carro").style.display = "block";
          document.getElementById("fondo").style.display = "block";

          document.body.classList.add("stop-scrolling"); 
          window.scrollTo(0, 0); 

          this.mostrarCarroBool = true;
        }
        else{
          document.getElementById("carro").style.display = "none";
          document.getElementById("fondo").style.display = "none";
          document.body.classList.remove("stop-scrolling");

          this.mostrarCarroBool = false; 
        }
      }
    }
  }

  //Carga los elementos del carro de compras desde el local storage
  var carritoCompleto = [];

    window.onload = function() {
      if (typeof(Storage) !== "undefined")
        carritoCompleto = JSON.parse(localStorage.getItem("Carrito"));

      if(carritoCompleto != null || carritoCompleto.lenght != 0)
        document.getElementById("puntito").style.display = "block";
      else
        document.getElementById("puntito").style.display = "none";
    };
</script>

<style lang="scss">
  @import "./styles/custom.scss";
  @import '../node_modules/bootstrap/scss/bootstrap.scss';

  .carro {
    width: fit-content;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    border-radius: 5px;
    -webkit-box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.18);
    -moz-box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.18);
    box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.18);
  }

  img {
    width: 50vh;
  }

  .iconoCarrito {
    position: relative;
    .puntito {
      width: 15px;
      height: 15px;
      position: absolute;
      z-index: 10;
      background-color: red;
      top: 0;
      right: 0;
      border-radius: 100%;
      display: none;
    }
  }

  .carro {
    display: none;
    width: 80vh;
    z-index: 20;
    background-color: white;
  }

  .cruz {
    position: absolute;
    right: -25px;
    top: -25px;
    opacity: 0.7;
  }

  #fondo {
    background-color: rgba(0,0,0,0.4);
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
    z-index: 15;
    display: none;
  }

  .stop-scrolling {
    overflow: hidden;
  }
</style>

