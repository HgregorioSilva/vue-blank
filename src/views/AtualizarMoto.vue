<template>
  <div>
    <form @submit.prevent="cadastrar">
      <h2>Altualizar Moto</h2>
      <div class="form-group">
        <label for="id">Id</label>
        <input
          type="text"
          id="id"
          class="form-control" required autofocus
          v-model="id">
      </div>
      <div class="form-group">
        <label for="placa">Placa</label>
        <input
          type="text"
          id="placa"
          class="form-control" required autofocus
          v-model="placa">
      </div>
      <div class="form-group">
        <label for="modelo">Modelo</label>
        <input
          type="text"
          id="modelo"
          class="form-control" required autofocus
          v-model="modelo">
      </div>
      <button class="btn btn-lg btn-primary btn-block" type="submit">
        Alterar
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import { mapState } from "vuex";


export default {
  name: "motos",
  data() {
    return {
      id: "",
      placa: "",
      modelo: "",
    };
  },
  computed: {
    ...mapState(["usuario"]),
    tk: {
        get() {
            return this.$store.state.token
        },
        set(value){
            this.setToken(value);
        }
    }
  },
  methods: {
    cadastrar() {
      axios
        .put("moto",  {
          id: this.id,
          placa: this.placa,
          modelo: this.modelo,
        },{ headers: { Accept: "application/json", Authorization: 'Bearer ' + this.tk} })
        .then((res) => {
          console.log(res);
          this.id = "";
          this.placa = "";
          this.modelo = "";
        })
        .catch((error) => console.log(error))
    },
  },
  
};
</script>