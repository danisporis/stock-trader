<template>
    <div class="row mt-3 mb-3">
        <app-stock v-for="stock in stocks" :stock="stock" :key="stock.id"></app-stock>        
    </div>
</template>

<script>
    import {mapGetters} from 'vuex'
    import Stock from './Stock.vue'

    export default {
        computed: {
            ...mapGetters({
                stocks: 'stockPortfolio'
            })
        },
        components: {
            appStock: Stock
        }
    }
</script>