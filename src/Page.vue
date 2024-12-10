<template>
    <div class="container">
        <header class="bottom">
            <page-header 
                v-model:filter="filter"
                v-model:pageAddView="pageAddView">
            </page-header>
        </header>
        <main>
            <page-main v-if="!pageAddView"
                v-model:filteredDatas="filteredDatas" 
                v-model:pageView="pageView"
                v-model:buyProduct="buyProduct"
                v-model:pageBuyView="pageBuyView">
            </page-main>
            <page-add v-if="pageAddView"
                v-model="productDatas"
                v-model:pageAddView="pageAddView">
            </page-add>
        </main>
    </div>
</template>

<script setup>
    import PageHeader from './components/PageHeader.vue';
    import PageMain from './components/PageMain.vue';
    import PageAdd from './components/PageAdd.vue';
    import {ref} from "vue";

    const pageView = defineModel('pageView')
    const buyProduct = defineModel('buyProduct')
    const filteredDatas = defineModel('filteredDatas')
    const filter = defineModel('filter')
    const pageBuyView = defineModel('pageBuyView')
    const productDatas = defineModel()

    const pageAddView = ref(false)
</script>

<style scoped>
    .bottom {
        margin-bottom: 40px;
    }
</style>