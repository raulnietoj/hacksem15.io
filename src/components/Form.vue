<template>
    <form @submit.prevent="frmSubmit" v-bind:class="'modal ' + (open == true ? 'open' : '')">
        <div class="container">
            <div class="row">
                <h2>Titulo</h2>
            </div>
            <div class="row">
                <label>
                    {{url.label}}
                    <input type="text" :placeholder="'Ingrese ' + url.label" v-model="url.valor" />
                </label>
            </div>
            <div class="row">
                <label>
                    {{titulo.label}}
                    <input type="text" :placeholder="'Ingrese ' + titulo.label" v-model="titulo.valor" />
                </label>
            </div>
            <div class="row">
                <label>
                    {{descripcion.label}}
                    <input type="text" :placeholder="'Ingrese ' + descripcion.label" v-model="descripcion.valor" />
                </label>
            </div>
            <div class="row buttons">
                <button type="button" v-text="boton.cerrar" @click.prevent="btnCerrar"></button>
                <button type="submit" v-text="boton.guardar"></button>
            </div>
        </div>
    </form>
</template>

<script>
export default {
    name: 'form-component',
    props: ['open', 'item'],
    data: () => {
        return {
            id: null,
            url: { label: 'URL', valor: null },
            titulo: { label: 'Título', valor: null },
            descripcion: { label: 'Descripción', valor: null },
            boton: { guardar: 'GUARDAR', cerrar: 'CERRAR' }
        }
    },
    watch: {
        item(newValue, oldValue) {
            this.id = newValue == null ? null : newValue.id;
            this.url.valor = newValue == null ? null : newValue.url;
            this.titulo.valor = newValue == null ? null : newValue.titulo;
            this.descripcion.valor = newValue == null ? null : newValue.descripcion;
        }
    },
    methods: {
        frmSubmit() {
            let data = {
                url: this.url.valor,
                titulo: this.titulo.valor,
                visualizaciones: 0,
                descripcion: this.descripcion.valor
            };

            let url = `http://localhost:3000/video${(this.id == null ? "" : `/${this.id}`)}`;
            let init = { method: this.id == null ? 'POST' : 'PUT', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(data) };

            fetch(url, init)
            .then(r => r.text())
            .then(this.mostrarResultadoRegistrarVideo);
        },
        btnCerrar() {
            this.$parent.open = false;
        },
        mostrarResultadoRegistrarVideo(data) {
            this.$parent.open = false;
            this.$parent.listar();
        }
    }
}
</script>

<style lang="scss" scoped>
#app {
    & .modal {
        display: none;

        &.open {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: absolute;
            background-color: rgba(229, 229, 229, 0.5);
            width: 100%;
            height: 100%;
        }

        & .container {
            background-color: white;
            box-shadow: black 0px 0px 3px;
            width: 50%;
            padding: 20px;
        }
    }
    & .row {
        display: flex;
        margin-bottom: 10px;
        width: 100%;

        & label {
            font-weight: bold;
            display: flex;
            width: 100%;
            flex-direction: column;

            & input {
                display: flex;
                padding: 5px 10px;
            }
        }

        &.buttons {
            display: flex;
            flex-direction: row;
            justify-content: space-evenly;

            & button {
                display: flex;
                padding: 5px 10px;
            }
        }
    }

    & .row:last-of-type {
        margin-bottom: 0;
    }
}
</style>