<template>
    <div>
        <HeaderComponent />
        <main class="main">
            <h2>Lista de videos</h2>
            <ListComponent v-bind:listado="lista" />
        </main>
        <FormComponent v-bind:open="open" v-bind:item="item" />
        <ConfirmacionComponent titulo="Mensaje" mensaje="¿Seguro de Eliminar Video?" confirm-text="Aceptar" cancel-text="Cancelar" v-bind:open="confirm" :cancel-callback="btnCancelarEliminar" :confirm-callback="btnConfirmarEliminar" />
    </div>
</template>

<script>
// @ is an alias to /src
import HeaderComponent from '@/components/Header.vue'
import ListComponent from '@/components/List.vue'
import FormComponent from '@/components/Form.vue'
import ConfirmacionComponent from  '@/components/Confirmacion.vue'

export default {
  name: 'Home',
  components: { HeaderComponent, ListComponent, FormComponent, ConfirmacionComponent },
  data: () => {
      return {
          lista: [],
          item: null,
          open: false,
          confirm: false
      };
    },
    methods: {
        btnConfirmarEliminar() {

        },
        btnCancelarEliminar() {

        },
        listar(){
            let url = 'http://localhost:3000/video';

            fetch(url)
                .then(r => r.json())
                .then(j => {
                    this.lista = j;
                });
        }
    },
    created() {
        // console.log(this);
        this.listar();
    }
}
</script>

<style lang="scss" scoped>

</style>