<template>
    <div>
        <div class="list headerList">
            <div> # </div>
            <div> Date </div>
            <div> Category </div>
            <div> Cost </div>
        </div>
        <div class="list" v-for="(item, index) in getPaymentListPage" :key="index">
            <div> {{ item.id }} </div>
            <div> {{ item.date }} </div>
            <div> {{ item.category }} </div>
            <div> {{ item.price }} </div>
        </div>      
    </div>
</template>

<script>
import { mapGetters } from 'vuex';
export default {
    computed: {
        ...mapGetters([
            'getPaymentList',
            'getPaymentListPage',
            'getItemNum'
        ])
    }

}
</script>

<style>
.list {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 15px;
    font-weight: 400;
    text-align: start;
    margin: 20px;
    width: 800px;
    display: grid;
    grid-template-rows: 40px;
    grid-template-columns: 10% 30% 30% 30%;
    border-bottom: 2px solid rgb(168, 166, 166);
}

.headerList {
    border-bottom: 3px solid rgb(57, 185, 117);
    font-weight: 600;
    color:seagreen;
}
</style>