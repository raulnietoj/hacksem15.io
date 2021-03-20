<template>
    <div  v-bind:class="'confirmacion ' + (open == true ? 'open' : '')">
        <div class="container">
            <div class="header">
                <h2 v-text="titulo"></h2>
            </div>
            <hr>
            <div class="content">
                <p v-text="mensaje"></p>
            </div>
            <hr>
            <div class="footer">
                <button v-text="confirmText" @click="btnConfirmClick"></button>
                <button v-text="cancelText" @click="btnCancelClick"></button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'confirmacion-component',
    props: ['open', 'titulo', 'mensaje', 'confirmText', 'cancelText', 'confirmCallback', 'cancelCallback'],
    methods: {
        btnConfirmClick() {
            this.$parent.confirm = false;
            this.confirmCallback();
        },
        btnCancelClick() {
            this.$parent.confirm = false;
            this.cancelCallback();
        }
    }
}
</script>

<style lang="scss" scoped>
#app { 
    & .confirmacion {
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
            & .container {
                background-color: white;
                box-shadow: black 0px 0px 3px;
                width: 50%;
                &>* {
                    padding: 10px 20px;
                }

                &>hr {
                    padding: 0px;
                }

                & .footer {
                    display: flex;
                    flex-direction: row;
                    justify-content: space-around;

                    & button{
                        padding: 10px;
                    }
                }
            }
        }
    }
}
</style>