<template>
<div>
    <div>
        <button class="formAddButton wrap" @click="changeViewForm">ADD NEW COST +</button>
        <div v-if="viewForm" class="formAdd">
            <input type="text" placeholder="Payment date" v-model="date">
            <input type="text" placeholder="Payment category" v-model="category">
            <input type="text" placeholder="Payment amount" v-model.number="price">
            <button class="formAddButton" @click="save">ADD +</button>
        </div>
    </div>
</div>

    

</template>

<script>
import { mapMutations } from 'vuex';

export default {
    data () {
        return {
            id: '',
            date: '',
            category: '',
            price: '',
            viewForm: false
        }
    },
    props: {
        items: Array
    },
    methods: {
        save () {
            const { date, category, price} = this;
            this.setPaymentsItem( { date, category, price} ) 
            // this.$emit('add', {date, category, price})
        },
        changeViewForm () {
            return this.viewForm = this.viewForm == false ? true : false;
        },
        ...mapMutations(['setPaymentsItem'])
    }
}
</script>

<style>
.formAdd {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 15px;
    font-weight: 400;
    text-align: start;
    margin: 20px;
    width: 400px;
    display: grid;
    grid-template-areas: 'row-1''row-2''row-3''row-4';
    grid-template-rows: repeat(4, 40px);
    row-gap: 10px;
    grid-template-columns: 1v;
    cursor: pointer;
}
.formAddButton {
    grid-area: row-4;
    width: 150px;
    background: mediumseagreen;
    color: white;
    border-color: white;
    border-radius: 10px;
    cursor: pointer;
}

.wrap {
    margin: 20px;
    height: 40px;
}
</style>