<template>
  <div>
    <form class="form">
      <div class="form-control">
        <label for="price-picker">Price</label>
        <vue-slider id="price-picker" ref="slider" v-model="priceRange" v-bind="sliderOptions"></vue-slider>
        <span class="small">From {{priceRange[0]}}lv. to {{priceRange[1]}}lv.</span>
      </div>
      <div class="form-control">
        <label class="typo__label">Vendor</label>
        <multiselect v-model="vendors" :options="vendorOptions" :multiple="true" :close-on-select="false" :clear-on-select="false" :preserve-search="true" placeholder="All Vendors" label="name" track-by="name" :preselect-first="true"></multiselect>
      </div>
    </form>
      <button class="btn-block btn-primary " @click="filterProducts()">Filter</button>
  </div>
</template>

<script>
  import vueSlider from 'vue-slider-component';
  import Multiselect from 'vue-multiselect';
  
  export default {
    components: {
      vueSlider,
      Multiselect
    },
    data() {
      return {
        sliderOptions: {
          min: 0,
          max: 2000,
          tooltip: 'hover',
          enableCross: false,
          minRange: 100
        },
        priceRange: [500, 2000],
        vendors: [],
        vendorOptions: [{
            name: 'Мебели Виденов',
            _id: 'Виденов'
          }, {
            name: 'Други Мебели',
            _id: 'Мебели'
          }
        ],
      };
    },
    props: ["product"],
    methods: {
      filterProducts() {
        const filter = {
          maxPrice: this.priceRange[1],
          minPrice: this.priceRange[0],
          vendors: this.vendors
        }
        this.$store.dispatch('updateProductFilter', filter);
      }
    }
  };
</script>
