<template>
    <li class="card">
        <div class="video">
            <div class="opciones">
                <a href="#" class="btnEditar" v-text="boton.editar" @click.prevent="btnEditarClick"></a>
                <a href="#" class="btnEliminar" v-text="boton.eliminar" @click.prevent="btnEliminarClick"></a>
            </div>
            <video class="url" controls>
                <source v-bind:src="item.url" />
            </video>
        </div>
        <div class="contenido">
            <div class="titulo" v-text="item.titulo"></div>
            <div class="visualizacion" v-text="item.visualizaciones + ' visualizaciones'"></div>
            <div class="descripcion" v-text="item.descripcion"></div>
        </div>
    </li>
</template>

<script>
export default {
    name: 'CardComponent',
    props: ['item'],
    data: () => {
        return {
            boton: { editar: 'Editar', eliminar: 'Eliminar' }
        }
    },
    methods: {
        btnEliminarClick() {
            this.$parent.$parent.confirm = true;
            this.$parent.$parent.btnCancelarEliminar = this.btnCancelar;
            this.$parent.$parent.btnConfirmarEliminar = this.btnConfirmar;
        },
        btnEditarClick() {
            let id = this.item.id;

            let url = `http://localhost:3000/video/${id}`;

            fetch(url)
                .then(r => r.json())
                .then(j => {
                    this.$parent.$parent.open = true;
                    delete j.visualizaciones;
                    this.$parent.$parent.item = j;
                    // this.$parent.$parent.$children[2].item = j;
                });
        },
        btnConfirmar() {
            let id = this.item.id;

            let url = `http://localhost:3000/video/${id}`;
            let init = { method: 'delete' };

            fetch(url, init)
                .then(r => r.json())
                .then(j => {
                    this.$parent.$parent.listar();
                });
        },
        btnCancelar() {
            console.log('dasdas');
        }
    }
}
</script>

<style lang="scss" scoped>
#app div >.main .info ul {
    & .card {
        display: flex;
        flex-direction: column;
        box-shadow: black 0px 0px 3px;


        & .video {
            display: flex;
            flex-direction: column;

            & .opciones {
                display: flex;
                flex-direction: row;
                justify-content: space-around;
            }

            & video {
                max-width: 100%;
                max-height: 100%;
            }
        }

        & >.titulo,
        .opciones a {
            font-size: 12px;
        }

        & .contenido {
            padding: 10px;

            & >.titulo,
            .visualizacion,
            .descripcion{
                font-size: 12px;
            }

            & .titulo {
                font-weight: bold;
            }

            & .descripcion {
                color: #808080;
            }

            & .visualizacion {
                color: #303030;
            }
        }
    }
}
</style>