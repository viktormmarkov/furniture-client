<template>
    <div>
        <div class="container">
            <div class="row">
                <div class="col-sm-3">
                    <FilterProduct></FilterProduct>
                </div>
                <div class="col-sm-9">
                    <Cards :products="products" />
                    <p class="text-center mb-0">{{currentPage+1 }} / {{ pages }}</p>
                    <ul class="pagination justify-content-center">
                        <li class="page-item" :class="{disabled: prevUrl === ''}">
                            <button class="page-link" @click="checkPage(prevUrl)">Previous</button>
                        </li>
                        <li class="page-item" :class="{disabled: nextUrl === ''}">
                            <button class="page-link" @click="checkPage(nextUrl)">Next</button>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Cards from './Cards';
    import FilterProduct from './FilterProduct';
    import Api from '@/config/Api';
    import _ from 'lodash';
    
    export default {
        components: {
            Cards,
            FilterProduct
        },
        data() {
            return {
                products: [],
                currentPage: '',
                pages: '',
                prevUrl: '',
                nextUrl: ''
            }
        },
        created() {
            Api().get('/products')
                .then(response => {
                    this.products = response.data.products;
                    this.currentPage = response.data.currentPage;
                    this.pages = response.data.pages;
                    this.nextUrl = response.data.nextUrl;
                    this.prevUrl = response.data.prevUrl;
                });
        },
        methods: {
            checkPage(url) {
                Api().get(url)
                    .then(response => {
                        this.products = response.data.products;
                        this.currentPage = response.data.currentPage;
                        this.pages = response.data.pages;
                        this.nextUrl = response.data.nextUrl;
                        this.prevUrl = response.data.prevUrl;
                    })
            }
        }
    }
</script>

<style scoped>
    
</style>
