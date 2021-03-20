<template>
    <header class="header">
        <div class="main">
            <a href="/" class="logo" v-text="titulo"></a>
            <a href="#" v-text="boton.agregar" @click.prevent="btnAgregarClick"></a>
        </div>
    </header>
</template>

<script>
export default {
    name: 'header-component',
    data: () => {
        return {
            titulo: 'VIDEO TV',
            boton: {
                agregar: 'AGREGAR'
            }
        }
    },
    methods: {
        btnAgregarClick() {
            // console.log(this);
            this.$parent.open = true;
            this.$parent.item = null;
        }
    }
}
</script>

<style lang="scss" scoped>
#app > div {
    &>.header {
    display: flex;
    width: 700px;
    margin: 0 auto;
    background-color: #FF5252;
    padding: 10px 40px;
        & .main {
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            align-items: center;
        }

        & a {
            color: white;
            text-shadow: black 0px 3px 3px;
            font-size: 13px;
        }

        & a.logo {
            font-size: 20px;
            font-weight: bold;
        }
    }
}
</style>