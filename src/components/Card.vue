<template>
  <div class="card" style="width: 100%; height:100%;">
    <div class="card-body">
        <router-link tag="a" :to="{name: 'product', params: {id: product._id}}">
            <img class="card-img-top" :src="product.image" :alt="product.name">
        </router-link>
        <h5 class="card-title text-info">{{ product.name }}</h5>
        <p class="card-text text-danger">{{ product.price }} лв.</p>
    </div>
</div>
</template>

<script>
import mixins from '@/mixins/mixins';
export default {
    props: ['product'],
    mixins: [mixins]
}
</script>

<style scoped>
.card-title {
        cursor: pointer;
    }
</style>
