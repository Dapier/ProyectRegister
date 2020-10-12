<template>
  <div>Hola</div>
</template>s
<script >
const firebase = require("firebase/app");
import { auth, database, messaging } from "firebase";
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
};
</script>

<style scoped>
</style>