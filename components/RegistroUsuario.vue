<template>
  <b-container>
    <Usuarios />
  </b-container>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import Usuarios from '~/components/Usuarios.vue';

@Component({
  components: { Usuarios }
})

export default class RegistroUsuario extends Vue { }
</script>