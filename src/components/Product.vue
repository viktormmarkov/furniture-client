<template>
  <div class="container">
    <div class="row">
      <div class="col-md-4">
        <img :src="product.image" :alt="product.name" class="img-fluid">
      </div>
      <div class="col-md-8">
        <h5>{{ product.name }}</h5>
        <p><span class="font-weight-bold">Category</span>: {{ product.category }}</p>
        <p class="text-danger font-weight-bold">{{product.price}} лв.</p>
        <p>
          {{ product.description }}
        </p>
        <p>
          {{ product.vendor }}
        </p>
        <p>
          <a :href="product.url">Виж оригинал</a>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import Api from '@/config/Api'
import mixins from '@/mixins/mixins'

export default {
  props: ['id'],
  mixins: [mixins],
  data(){
    return {
      product: {}
    }
  },
  created() {
       Api().get(`/products/${this.id}`)
              .then(response => {
                this.product = response.data
              });
  },
  methods: {
        checkout(e) {
            e.preventDefault();
            this.$router.push({ name: 'checkout' });
        }
    }
}
</script>

<style>

</style>
