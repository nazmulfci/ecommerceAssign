<script setup>
import { ref, watch } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute();
let url = route.params.id;
const id = ref();
id.value = url;

// console.log(window.location.search);
watch(()=>route.params.id,(newValue)=>{
  console.log(newValue);
  // let url = new URLSearchParams(window.location.search).get('id');
  id.value = newValue;
  getdata();
})

const data = ref();

async function getdata() {
  const response = await fetch("https://dummyjson.com/products");
   data.value = await response.json();
 // console.log(data);
}

getdata();
</script>

<template>
  <div class="about">
    <h1>Product List </h1>
  </div>
  <hr>
<!-- {{ data }} -->
  <div class="row">
    <div class="col-md-3 mb-3" v-for="item in data.products" :key="item.id">
        <RouterLink :to="`/productDetails/${item.id}`">
    <div class="">
       <div class="card">
        <img class="card-img-top" :src="item.thumbnail" :alt="item.title">  
        <div class="card-body">
          <p class="card-text"> {{ item.title }} </p>
          <p class="card-text text-danger"> Price : {{ item.price }} </p>
          <p class="card-text text-success"> Brand : {{ item.brand }} </p>
        </div>
        </div>

      </div>
    </RouterLink>
    </div>
  </div>

  <!-- {{ data }} -->
</template>
