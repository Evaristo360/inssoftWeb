<template>
  <div class="m-2">
    <registro @usuario-registrado="actualizarTabla"></registro>
    <b-table striped hover :items="items"></b-table>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import axios from 'axios';
import Registro from './Registro.vue';

interface Usuario {
  age: number;
  first_name: string;
  last_name: string;
}

@Component
export default class MyClass extends Vue {
  items: Usuario[] = [];
  actualizando = false;

  mounted(): void {
    this.obtenerDatos();
  }

  obtenerDatos(): void {
    axios.get('http://localhost:8020/User')
      .then((response: any) => {
        this.items = response.data;
      })
      .catch((error: any) => {
        console.error(error);
      });
  }

  actualizarTabla(): void {
    if (!this.actualizando) {
      this.actualizando = true;
      this.obtenerDatos();
      setTimeout(() => {
        this.actualizando = false;
      }, 1000);
    }
  }
}
</script>