<template>
    <h4>Информация о товаре</h4>
    <div class="margin">
        <div class="ileft"><label>Наименование:</label></div>
        <div class="iright"><input type="text" class="mleft" v-model="prodName" /></div>
        <div class="icenter"></div>
        <div class="iclear"></div>
    </div>
    <div class="margin">
        <div class="ileft"><label>Цена:</label></div>
        <div class="iright"><input type="number" class="mleft" v-model="prodPrice" /></div>
        <div class="icenter"></div>
        <div class="iclear"></div>
    </div>
    <div class="margin">
        <div class="ileft"><label>Описание:</label></div>
        <div class="iright"><textarea class="mleft" v-model="prodDescr"></textarea></div>
        <div class="icenter"></div>
        <div class="iclear"></div>
    </div>
    <div class="margin">
        <div class="ileft"><label>Категория:</label></div>
        <div class="iright"><input type="text" class="mleft" v-model="prodCtgr" /></div>
        <div class="icenter"></div>
        <div class="iclear"></div>
    </div>
    <div class="margin">
        <div class="ileft"><label>Рейтинг:</label></div>
        <div class="iright"><input type="number" class="mleft" v-model="prodRating" /></div>
        <div class="icenter"></div>
        <div class="iclear"></div>
    </div>
    <div class="margin">
        <div class="ileft"><label>Количество проголосовавших:</label></div>
        <div class="iright"><input type="number" class="mleft" v-model="prodCount" /></div>
        <div class="icenter"></div>
        <div class="iclear"></div>
    </div>
    <div class="margin">
        <div class="ileft"><label>Ссылка на изображение:</label></div>
        <div class="iright"><input type="text" class="mleft" v-model="prodLink" /></div>
        <div class="icenter"></div>
        <div class="iclear"></div>
    </div>
    <hr>
    <button @click="add()">Добавить</button>
</template>

<script setup>
    import {ref} from "vue";
    
    const productDatas = defineModel()
    const pageView = defineModel('pageView')
    const pageAddView = defineModel('pageAddView')

    const prodName = ref('')
    const prodPrice = ref(null)
    const prodDescr = ref('')
    const prodCtgr = ref('')
    const prodRating = ref(null)
    const prodCount = ref(null)
    const prodLink = ref('')
    const prodId = ref(productDatas.value.length)

    function add() {
        if (prodName !== '') {
            prodId.value += 1
            productDatas.value.push({id: prodId.value,
                                    title: prodName.value,
                                    price: prodPrice.value,
                                    description: prodDescr.value,
                                    category: prodCtgr.value,
                                    image: prodLink.value,
                                    rating: {rate: prodRating.value, count: prodCount.value}
            })
        }
        pageAddView.value = false
        pageView.value = true
    }
</script>

<style scoped>
    div {
        display: block;
    }

    .ileft {
        float: left;
    }

    .iright {
        float: right;
    }

    .icenter {
        text-align: center; 
        margin: 0 auto;
    }

    .iclear {
        clear: both;
    }

    .margin {
        margin: 5px;
    }

    .mleft {
        margin-left: 10px;
    }
</style>