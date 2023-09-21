<script setup>
import { onMounted, reactive, ref } from 'vue'
import { useRoute } from 'vue-router';




// best practice
// - onMounted hook have to use at mounting component.




// initialize with default object. Because at first when template is rendering, postDetails object is necessary.
// let data = ref({
//   postDetails:{
//     title:'',
//     img:'#',
//     content:"dummy"
//   }
// });

const route = useRoute();
let id =route.params.id// new URLSearchParams(window.location.search).get('id'); //route.query.id

const data = ref();

async function getdata() {
    fetch('https://dummyjson.com/products/'+id)
.then(res => res.json())
.then(json => data.value = json)
}

getdata();
</script>

<template>


<!-- {{ data }} -->
<div class="container">
  <div class="about">
    <h4>In Detail of
      <span>{{  data.title }}</span></h4>
  </div>
  <hr>


  <div class="row">
    <div class="col-md-6">

      <div class="card">
        <img class="card-img-top" :src="data.thumbnail" :alt="data.title">
        <div class="row">
        <div class="col-md-2 text-center" v-for="img in data.images">
            <center>
            <img class="img img-thumbnail" :src="img" style="height: 70px;">
        </center>
        </div>
        </div>

      </div>

    </div>

    <div class="col-md-6">
        <h1> {{ data.title }} </h1>
        <p> {{ data.description }} </p>
        <p> 
            <span v-if="data.stock>0" class="badge badge-success"> In Stock </span>
            <span v-else class="badge badge-danger"> Out of Stock </span>
         </p>
        <p class="text-danger"> Price : {{ data.price }} </p>
        <p class="text-success"> Brand : {{ data.brand }} </p>
        <p class=""> Category : {{ data.category }} </p>
    </div>
  </div>
  </div>
</template>
