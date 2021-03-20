<template>
    <div class="info">
        <div v-if="listado.length == 0">No existe información</div>
        <ul v-else>
            <CardComponent v-for="x in listado" v-bind:item="x" v-bind:key="x.id" />
        </ul>
    </div>
</template>

<script>
import CardComponent from '@/components/Card.vue';
export default {
    name: 'list-component',
    components: {CardComponent},
    props: ['listado'],
}
</script>

<style lang="scss" scoped>
#app div {
    &>.main .info {
        display: flex;
        flex-direction: column;
        width: 100%;
        &>div {
            margin-top: 20px;
            align-self: center;
        }
        & ul {
            display: grid;
            grid-gap: 10px;
            grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
        }
    }
}
</style>