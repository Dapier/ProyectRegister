<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light eventoFime">
      Eventos FIME

      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav">
          <li class="corner">Bienvenido de vuelta {{ name }}</li>

          <button
            class="btn btn-outline-success my-2 my-sm-0 datosButton"
            role="button"
            @click="accessData"
          >
            Datos
          </button>

          <button
            class="btn btn-outline-danger my-2 my-sm-0 botonLogout"
            role="button"
          >
            <a class="nav-item botonCerrar" href="/#/" @click="logOut">
              Salir
            </a>
          </button>
        </ul>
      </div>
    </nav>

    <div class="row m-0 p-0">
      <div class="card" style="width: 20rem">
        <img
          class="card-img-top"
          src="../assets/evento 1.jpg"
          alt="Card image cap"
        />
        <div class="card-body">
          <h2>Code For All</h2>
          <p class="card-text">
            No te pierdas el mejor evento para aprender a programar desde 0
          </p>
          <a href="#" class="card-link">Asistire!</a>
        </div>
      </div>

      <div class="card" style="width: 20rem">
        <img
          class="card-img-top"
          src="../assets/programming.jpg"
          alt="Card image cap"
        />
        <div class="card-body">
          <h2>Python Fest</h2>
          <p class="card-text">
            Aprende, diviertete y convive en el Pyhton Fest
          </p>
          <a href="#" class="card-link">Asistire!</a>
        </div>
      </div>

      <div class="card" style="width: 20rem">
        <img
          class="card-img-top"
          src="../assets/hacking.jpg"
          alt="Card image cap"
        />
        <div class="card-body">
          <h2>Hackatron</h2>
          <p class="card-text">
            Compite contra los mejores hackers y demuestra tu talento
          </p>
          <a href="#" class="card-link">Asistire!</a>
        </div>
      </div>

      <div class="card" style="width: 20rem">
        <img
          class="card-img-top"
          src="../assets/javascript.png"
          alt="Card image cap"
        />
        <div class="card-body">
          <h2>Taller Javascript</h2>
          <p class="card-text">
            Aprende uno de los lenguajes top, totalmente gratis!
          </p>
          <a href="#" class="card-link">Asistire!</a>
        </div>
      </div>

      <div class="card" style="width: 20rem">
        <img
          class="card-img-top"
          src="../assets/scrach.png"
          alt="Card image cap"
        />
        <div class="card-body">
          <h2>Programacion para niños</h2>
          <p class="card-text">
            Lleva a tus hijos a aprender a programar de una manera divertida
          </p>
          <a href="#" class="card-link">Asistire!</a>
        </div>
      </div>

      <div class="card" style="width: 20rem">
        <img
          class="card-img-top"
          src="../assets/java.png"
          alt="Card image cap"
        />
        <div class="card-body">
          <h2>Taller de Programacion orientada a objetos</h2>
          <p class="card-text">Aprende POO para dar un plus a tu CV !</p>
          <a href="#" class="card-link">Asistire!</a>
        </div>
      </div>
    </div>
  </div>
  <!--Eventos-->
</template>

<script>
import { auth, database } from "firebase";
import { Auth } from "../firebase/auth.js";

const firebase = require("firebase/app");
require("firebase/database");
import HomePage from "../components/HomePage";

export default {
  data() {
    return {
      title: "registro Fime",
      email: "",
      message: "",
      name: "",
      phone: "",
      matricula: "",
      folio: "",
    };
  },
  methods: {
    logOut() {
      firebase
        .auth()
        .signOut()
        .then(function () {
          this.$router.replace({ name: "Eventos" });
        })
        .catch(function (error) {
          console.log("error");
        });
    },
    accesData() {
      this.$router.replace({ name: "Datos" });
    },
  },
};
</script>
<style scoped>
body {
  background: inherit, white;
}
.datosButton {
  margin-left: 34rem;
  margin-top: 1rem;
}

.eventoFime {
  font-size: 1.5rem;
}

.corner {
  margin-left: 25vw;
  font-size: 1.5rem;
  margin-top: 0.2rem;
}
.botonLogout {
  margin-left: 10rem;
}
.botonCerrar {
  text-decoration: none;
  color: red;
}
.botonCerrar a :hover {
  color: white;
}
.datosButton {
  margin-left: 10rem;
}
.textDatos {
  text-decoration: none;
  color: black;
}

.card {
  margin: 4rem;
  margin-left: 5rem;
  margin-top: 4rem;
}
</style>