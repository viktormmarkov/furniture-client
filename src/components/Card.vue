<template>
  <div class="card" style="width: 100%; height:100%;">
    <div class="card-body">
        <router-link tag="a" :to="{name: 'product', params: {id: product._id}}">
            <img class="card-img-top" :src="product.image" :alt="product.name">
        </router-link>
        <h5 class="card-title text-info">{{ product.name }}</h5>
        <p class="card-text text-danger">{{ product.price }} лв.</p>
        <div class="row" style="height:15px">
            <div class="col-md-3 mb-1" v-for="color in colors" :key="color" v-bind:style="{ backgroundColor: color}">
            </div>
      </div>
    </div>
</div>
</template>

<script>
import mixins from "@/mixins/mixins";

export default {
  data() {
    return {
      colors: ["#7c6155", "#dfd1c4", "#372920", "#c1b1af"]
    };
  },
  props: ["product"],
  mixins: [mixins]
};
</script>

<style scoped>
.card-title {
  cursor: pointer;
}
</style>
