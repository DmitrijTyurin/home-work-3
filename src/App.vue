<template>
  <h1>Магазин</h1>
  <Page v-if="pageView" 
        v-model="productDatas"
        v-model:filteredDatas="filteredDatas" 
        v-model:pageView="pageView"
        v-model:buyProduct="buyProduct"
        v-model:filter="filter"
        v-model:pageAddView="pageAddView"
        v-model:pageBuyView="pageBuyView"/>
  <PageAdd v-if="pageAddView"
           v-model="productDatas"
           v-model:pageView="pageView"
           v-model:pageAddView="pageAddView"/>
  <PageBuy v-if="pageBuyView"
           v-model="productDatas"
           v-model:pageView="pageView"
           v-model:pageBuyView="pageBuyView"
           v-model:buyProduct="buyProduct"/>
  <p>&copy; 2024 Сделано на коленке, но с душой</p>
</template>

<script setup>
  import axios from "axios";
  import {onMounted, ref, computed} from "vue";
  import Page from './Page.vue';
  import PageAdd from "./PageAdd.vue";
  import PageBuy from "./PageBuy.vue";

  const pageView = ref(true)
  const pageAddView = ref(false)
  const pageBuyView = ref(false)
  const buyProduct = ref()

  const productDatas = ref ([])
  function getProductData() {
  axios
    .get("https://fakestoreapi.com/products")
    .then(response => (productDatas.value = response.data));
  }
  
  const filter = ref ({sName: '', sPriceFrom: null, sPriceTo: null})
  const filteredDatas = computed(() => {
    if (filter.value.sName !== '' || (filter.value.sPriceFrom !== null & filter.value.sPriceFrom !== '') || (filter.value.sPriceTo !== null & filter.value.sPriceTo !== ''))
      return productDatas.value.filter((productData) => 
              (filter.value.sName === '' || (filter.value.sName !== '' & productData.title.toLowerCase().includes(filter.value.sName.toLowerCase()))) &
              (filter.value.sPriceFrom === null || (filter.value.sPriceFrom !== null & productData.price >= filter.value.sPriceFrom)) &
              (filter.value.sPriceTo === null || (filter.value.sPriceTo !== null & productData.price <= filter.value.sPriceTo))
          )
    return productDatas.value
  })

  onMounted(() => {
      getProductData()
    })
</script>