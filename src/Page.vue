<template>
    <div class="container">
        <header class="bottom">
            <page-header 
                v-model:filter="filter"
                v-model:pageView="pageView"
                v-model:pageAddView="pageAddView">
            </page-header>
        </header>
        <main>
            <page-main 
                v-model:filteredDatas="filteredDatas" 
                v-model:pageView="pageView"
                v-model:buyProduct="buyProduct"
                v-model:pageBuyView="pageBuyView">
            </page-main>
        </main>
    </div>
</template>

<script setup>
    import PageHeader from './components/PageHeader.vue';
    import PageMain from './components/PageMain.vue';

    const pageView = defineModel('pageView')
    const buyProduct = defineModel('buyProduct')
    const filteredDatas = defineModel('filteredDatas')
    const filter = defineModel('filter')
    const pageAddView = defineModel('pageAddView')
    const pageBuyView = defineModel('pageBuyView')
</script>

<style scoped>
    .bottom {
        margin-bottom: 40px;
    }
</style>