<template>
    <div >
        <button v-for="page in pageNum" 
        :key="page"
        @click="setPage(page - 1)"
        class="pageNumber"
        >
        {{ page }}
        </button>

    </div>
</template>

<script>

import { mapMutations, mapGetters } from 'vuex';


export default {
    methods: {
        ...mapMutations(['setPage'])
    },
    computed: {
        ...mapGetters(['getItemNum','getPage']),
        pageNum() {
            return Math.ceil(this.getItemNum / 5)
        }
    }

}
</script>

<style>
.pageNumber {
    margin: 1px;
    color: white;
    font-weight: 700;
    background-color: mediumseagreen;
    border: 1px solid white;
    cursor: pointer;
    outline: none;
}
.pageNumber:hover {
    color: mediumseagreen;
    background-color: white;
}
.pageBtnCur {
    text-decoration: underline;
}

</style>
