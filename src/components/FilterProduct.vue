<template>
  <div class="form-vertical">
    <div class="form-control">
      <label for="price-picker">Price</label>
      <vue-slider id="price-picker" ref="slider" v-model="priceRange" v-bind="sliderOptions"></vue-slider>
      <span class="small"> From {{priceRange[0]}}lv. to {{priceRange[1]}}lv.</span>
    </div>
    <div class="form-control">
      <label class="typo__label">Vendor</label>
      <multiselect v-model="vendor" :options="vendorOptions" :multiple="true" :close-on-select="false" :clear-on-select="false" :preserve-search="true" placeholder="All Vendors" label="name" track-by="name" :preselect-first="true">
      </multiselect>
    </div>
  </div>
</template>

<script>
  import vueSlider from 'vue-slider-component';
  import Multiselect from 'vue-multiselect';
  import mixins from "@/mixins/mixins";
  
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
        vendor: [],
        vendorOptions: [{
            name: 'Vue.js',
            language: 'JavaScript'
          },
          {
            name: 'Rails',
            language: 'Ruby'
          },
          {
            name: 'Sinatra',
            language: 'Ruby'
          },
          {
            name: 'Laravel',
            language: 'PHP'
          },
          {
            name: 'Phoenix',
            language: 'Elixir'
          }
        ],
      };
    },
    props: ["product"],
    mixins: [mixins]
  };
</script>
