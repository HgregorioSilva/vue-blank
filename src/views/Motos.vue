<template>
  <div>
    <form @submit.prevent="cadastrar">
      <h2>Moto</h2>
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
        <textarea id="modelo" class="form-control" required v-model="modelo">
        </textarea>
      </div>
      <button class="btn btn-lg btn-primary btn-block" type="submit">
        Salvar
      </button>
    </form>
    <br />
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Id</th>
          <th>Placa</th>
          <th>Modelo</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="moto in motos" :key="moto.id">
          <td>{{ moto.id }}</td>
          <td>{{ moto.placa }}</td>
          <td>{{ moto.modelo }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import { mapState } from "vuex";


export default {
  name: "motos",
  data() {
    return {
      placa: "",
      modelo: "",
      motos: [],
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
        .post("moto", {
          placa: this.placa,
          modelo: this.modelo,
        })
        .then((res) => {
          console.log(res);
          this.placa = "";
          this.modelo = "";
          this.atualizar();
        })
        .catch((error) => console.log(error))
    },
    atualizar() {
      axios
        .get("moto", { headers: { Accept: "application/json", Authorization: 'Bearer ' + this.tk} })
        .then((res) => {
          console.log(res);
          this.motos = res.data;
        })
        .catch((error) => {
            alert(error.response.status)
        });
    },
  },
  created() {
    this.atualizar();
  },
};
</script>
