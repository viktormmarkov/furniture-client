<template>
    <div>
        <div class="container">
            <div class="row">
                <div class="col-sm-3">
                    <div class="form-control">
                        <label for="price-picker">Price</label>
                        <vue-slider id="price-picker" ref="slider" v-model="priceRange" v-bind="options"></vue-slider>
                        <span class="small"> From {{priceRange[0]}}lv to {{priceRange[1]}}lv</span>
                    </div>
                </div>
                <div class="col-sm-9">
                    <Cards :products="products" v-bind:filter="priceRange" />
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
    import Api from '@/config/Api';
    import vueSlider from 'vue-slider-component';
    import _ from 'lodash';
    
    export default {
        components: {
            Cards,
            vueSlider
        },
        data() {
            return {
                options: {
                    min: 0,
                    max: 2000,
                    tooltip: 'hover',
                    enableCross: false,
                    minRange: 100
                },
                priceRange: [500, 2000],
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
