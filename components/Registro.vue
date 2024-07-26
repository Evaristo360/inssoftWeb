<template>
  <b-card class="m-2">
    <h1>Registro de usuario</h1>
    <b-form @submit.prevent="registrarUsuario">
      <b-form-group label="Nombre" label-for="name">
        <b-form-input id="name" v-model="usuario.name" type="text" required></b-form-input>
      </b-form-group>
      <b-form-group label="Email" label-for="email">
        <b-form-input id="email" v-model="usuario.email" type="email" required></b-form-input>
      </b-form-group>
      <b-form-group label="Teléfono" label-for="phone">
        <b-form-input id="phone" v-model="usuario.phone" type="number" required></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">Registrar</b-button>
    </b-form>
  </b-card>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import axios from 'axios';

interface Usuario {
  name: string;
  email: string;
  phone: string;
}

@Component
export default class Registro extends Vue {
  usuario: Usuario = {
    name: '',
    email: '',
    phone: ''
  };

  registrarUsuario() {
    axios.post('http://localhost:8020/User', this.usuario)
      .then((response) => {
        console.log(response);
        this.$emit('usuario-registrado'); // Emitir evento
      })
      .catch((error) => {
        console.error(error);
      });
  }
}
</script>
