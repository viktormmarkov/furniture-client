<template>
    <div class="container">
        <div class="row">
            <div class="col-md-4 mb-3" v-for="product in filterItems(products, filter)" :key="product._id">
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
            filterItems: (products, filter) => {
                const min = _.min(filter);
                const max = _.max(filter);
                return _.filter(products, p => {
                    return (p.price > (min || 0) && p.price < (max || 2000));
                });
            }
        }
    
    }
</script>

<style scoped>
    
</style>
