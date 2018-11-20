<template>
    <div class="container">
        <div class="row">
            <div class="col-md-4 mb-3" v-for="product in filterItems(products)" :key="product._id">
                <Card :product="product" />
            </div>
        </div>
    </div>
</template>

<script>
    import Card from './Card';
    import _ from 'lodash';
    
    export default {
        props: ['products', 'filter'],
        components: {
            Card
        },
        methods: {
            filterItems: (products) => {
                return _.filter(products, () => true);
            }
        }
    
    }
</script>

<style scoped>
    
</style>
