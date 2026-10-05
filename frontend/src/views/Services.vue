<script setup lang="ts">
  import { ref, onMounted, computed } from 'vue';
  import type { Product } from '../stores/Product';
  import ProductList from '../components/ProductList.vue';
  import Typed from 'typed.js';

  const products = ref<Product[]>([]);
  const keyword = ref('');
  const sort = ref('');
  const hotProducts = ref<Product[]>([]);  
const category1Products = ref<Product[]>([]);  
const category2Products = ref<Product[]>([]); 

  onMounted(async () =>{
    const response = await fetch('http://localhost:3000/products');
    products.value = await response.json();
    console.log(products);
    hotProducts.value = await fetch('http://localhost:3000/products?hot=1')  
        .then(response => response.json());  
    category1Products.value = await fetch('http://localhost:3000/products?category=1')  
        .then(response => response.json());  
    category2Products.value = await fetch('http://localhost:3000/products?category=2')  
        .then(response => response.json());  
  });

  const filteredAndSortedProducts = computed(() => {
    let filteredProducts = products.value.filter(product =>
      product.name.toLowerCase().includes(keyword.value.toLowerCase())
    );
    if (sort.value === 'asc') {
      filteredProducts.sort((a, b) => a.price - b.price);
    }else{
      filteredProducts.sort((a, b) => b.price - a.price);
    }
    return filteredProducts; 
  });
</script>


<template>
  <div>
    
    <!-- <div class="row mt-3"> 
      <div class="col-md-3" v-for="product in filteredAndSortedProducts" :key="product.id">
        <div class="card mb-4">
            <img :src="'/images/'+product.image" class="h-5 w-55">
          <div class="card-body">
            <p><i class="bi bi-hand-thumbs-up"></i>{{ product.name }}</p>
            <p>{{ product.price }}</p>
            <p>{{ product.duration}}</p>
            <div class="text-center">
                        <RouterLink :to="'/detail/'+ product.id" class="btn btn-primary">Mua</RouterLink>
                    </div>
          </div>
        </div>
      </div>
    </div> -->
    <div class="container mt-5">
      <div class="row md-4 mt-3 d-flex justify-content-between">
      <div class="col-md-2 ms-2 ">
        <input v-model="keyword" type="text" placeholder="Tim kiem san pham" class="form-control">
      </div>
      <div class="col-md-2 me-2">
        <select v-model="sort" class="form-control">
          <option value="" disabled selected>Sap xep theo gia</option>
          <option value="asc">gia tang dan</option>
          <option value="desc">gia giam dan</option>
        </select>
      </div>
    </div>
      <div id="carouselExample" class="carousel slide carousel-dark" data-bs-ride="carousel">  
                <div class="carousel-indicators">  
                    <button type="button" data-bs-target="#carouselExample" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>  
                    <button type="button" data-bs-target="#carouselExample" data-bs-slide-to="1" aria-label="Slide 2"></button>  

                </div>  
                <div class="carousel-inner">  
                <button class="carousel-control-prev  " type="button" data-bs-target="#carouselExample" data-bs-slide="prev">  
                    <span ><i class="bi bi-arrow-left-circle"></i></span>  
                    <span class="visually-hidden">Previous</span>  
                </button>  
                <button class="carousel-control-next " type="button" data-bs-target="#carouselExample" data-bs-slide="next">  
                    <span aria-hidden="true"><i class="bi bi-arrow-right-circle-fill"></i></span>  
                    <span class="visually-hidden">Next</span>  
                </button>  
            </div>
                <div>
                    <ProductList title="Rubik Hot" :products="hotProducts" />  
                    <ProductList title="Rubik Cơ Bản" :products="category1Products" />  
                    <ProductList title="Rubik Biến Thể" :products="category2Products" />  
                </div>
            </div>
    </div>
  </div>
 
</template>



  

  
 
  
  