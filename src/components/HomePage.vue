<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-3 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <h4 class="card-title text-center">Hackaton FIME</h4>
            <h4 class="card-title text-center">Registrate</h4>
            <form @submit.prevent="addEmail(email, folio)" class="form-signin">
              <!--Nombre-->
              <div class="form-label-group form-group">
                <input
                  v-model="name"
                  id="nombre"
                  type="text"
                  class="form-control is valid"
                  placeholder="Nombre "
                  required
                  autofocus
                />
                <label for="nombre">Nombre</label>
              </div>

              <!--Email-->
              <div class="form-label-group">
                <input
                  v-model="email"
                  type="email"
                  id="Email"
                  class="form-control is valid"
                  placeholder="Email address"
                  required
                  autofocus
                />
                <label for="Email">Email</label>
              </div>

              <!--Telefono-->
              <div class="form-label-group">
                <input
                  v-model="phone"
                  type="tel"
                  id="telefono"
                  class="form-control"
                  required
                  placeholder="Tu numero de celular"
                />
                <label for="telefono">Celular</label>
              </div>

              <!--Matricula-->
              <div class="form-label-group">
                <input
                  v-model="matricula"
                  type="text"
                  id="matricula"
                  required
                  class="form-control"
                  placeholder="Matricula"
                />
                <label for="matricula">Matricula</label>
              </div>

              <div>{{ message }}</div>

              <button
                id="alerta"
                class="btn btn-lg btn-primary btn-block text-uppercase"
                type="submit"
              >
                Registrarse
              </button>
              <br />
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { auth, database, messaging } from "firebase";
import { Auth } from "../firebase/auth.js";

const firebase = require("firebase/app");
require("firebase/database");
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
    async addEmail(email) {
      var folioGenerado = "folio:" + this.generarFolio(10);
      var database = firebase.database();

      await Auth.createUserWithEmailAndPassword(email, folioGenerado),
        alert("Cuenta registrada tu folio es: " + folioGenerado);
      this.$router.replace({ name: "Eventos" }).catch(function (error) {
        alert("Ya esta registrado este correo");
        return;
      });

      this.correo = "";
      this.numeroMatricula = "";
      this.telefono = "";
      this.nombre = "";
      this.folio = folioGenerado;

      database.ref("/user").set({
        username: this.name,
        correo: this.email,
        numeroMatricula: this.matricula,
        telefono: this.phone,
      });
      return this.folio;
    },

    generarFolio(length) {
      var chars =
        "abcdfghijklmñopqrstuvwxyzABCDEFGHIJKLMÑOPQRSTUVWXYZ1234567890";
      var folio = "";
      for (var x = 0; x < length; x++) {
        var i = Math.floor(Math.random() * chars.length);
        folio += chars.charAt(i);
      }
      return (this.folio = folio);
    },
  },
};
</script>

<style >
:root {
  --input-padding-x: 1.5rem;
  --input-padding-y: 0.75rem;
}

body {
  width: 100vw;
  height: 100vh;
  background: url("../assets/night.jpg") no-repeat center center;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

.card-signin {
  border: 0;
  border-radius: 1rem;
  box-shadow: 0 0.5rem 1rem 0 rgba(0, 0, 0, 0.1);
}

.card-signin .card-title {
  margin-bottom: 2rem;
  font-weight: 300;
  font-size: 1.5rem;
}

.card-signin .card-body {
  padding: 2rem;
}

.form-signin {
  width: 100%;
}

.form-signin .btn {
  font-size: 80%;
  border-radius: 5rem;
  letter-spacing: 0.1rem;
  font-weight: bold;
  padding: 1rem;
  transition: all 0.2s;
}

.form-label-group {
  position: relative;
  margin-bottom: 1rem;
}

.form-label-group input {
  height: auto;
  border-radius: 2rem;
}

.form-label-group > input,
.form-label-group > label {
  padding: var(--input-padding-y) var(--input-padding-x);
}

.form-label-group > label {
  position: absolute;
  top: 0;
  left: 0;
  display: block;
  width: 100%;
  margin-bottom: 0;
  /* Override default `<label>` margin */
  line-height: 1.5;
  color: #495057;
  border: 1px solid transparent;
  border-radius: 0.25rem;
  transition: all 0.1s ease-in-out;
}

.form-label-group input::-webkit-input-placeholder {
  color: transparent;
}

.form-label-group input:-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-moz-placeholder {
  color: transparent;
}

.form-label-group input::placeholder {
  color: transparent;
}

.form-label-group input:not(:placeholder-shown) {
  padding-top: calc(var(--input-padding-y) + var(--input-padding-y) * (2 / 3));
  padding-bottom: calc(var(--input-padding-y) / 3);
}

.form-label-group input:not(:placeholder-shown) ~ label {
  padding-top: calc(var(--input-padding-y) / 3);
  padding-bottom: calc(var(--input-padding-y) / 3);
  font-size: 12px;
  color: #777;
}

.btn-google {
  color: white;
  background-color: #ea4335;
}

.btn-facebook {
  color: white;
  background-color: #3b5998;
}

/* Fallback for Edge
-------------------------------------------------- */

@supports (-ms-ime-align: auto) {
  .form-label-group > label {
    display: none;
  }
  .form-label-group input::-ms-input-placeholder {
    color: #777;
  }
}

/* Fallback for IE
-------------------------------------------------- */

@media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
  .form-label-group > label {
    display: none;
  }
  .form-label-group input:-ms-input-placeholder {
    color: #777;
  }
}
</style>