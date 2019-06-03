<template>
    <div class="container">
        <div class="row">
            <div class="col-md-4 mb-3" v-for="product in filteredItems" :key="product._id">
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
        computed: {
            productFilter: function() {
                return this.$store.getters.getProductFilter;
            },
            filteredItems: function(products) {
                const filter = this.$store.getters.getProductFilter;
                const {
                    minPrice,
                    maxPrice,
                    vendors
                } = filter;
                return _.filter(this.products, p => {
                    return (!minPrice || p.price > minPrice) &&
                        (!maxPrice || p.price < maxPrice) && 
                        (_.isEmpty(vendors) || _.includes(_.map(vendors, v => v.name), p.vendor));
                });
            }
        }
    }
</script>

<style scoped>
    
</style>
