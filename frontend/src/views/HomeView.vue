
<script setup lang="ts">
import { ref, onMounted } from 'vue';
import ProductList from '../components/ProductList.vue';
import type { Product } from '../stores/Product'; 
import Typed from 'typed.js';

const hotProducts = ref<Product[]>([]);  
const category1Products = ref<Product[]>([]);  
const category2Products = ref<Product[]>([]); 

onMounted(async () => {  
    hotProducts.value = await fetch('http://localhost:3000/products?hot=1')  
        .then(response => response.json());  
    category1Products.value = await fetch('http://localhost:3000/products?category=1')  
        .then(response => response.json());  
    category2Products.value = await fetch('http://localhost:3000/products?category=2')  
        .then(response => response.json());  
}); 

let typedInstance: Typed | null = null; // Declare typedInstance as a typed.js object or null initially

</script>

<template>
  <main>
    <div class="container" style="background-color: #6998AB;">
        <div class="hero" >
            <div class="container">
                <div class="row align-items-center">
                    <div class="row">
                        <div class="col-md-3"></div>
                        <div class="col-md-9">
                            <div class="row">
                                <div class="col-9 ">
                                    <img src="/images/thuong-hieu-rubik-1628873441.jpg" class="img-fluid" alt="">
                                </div>
                                <div class="col-3 px-0 ">
                                    <img src="/images/ads-righthome-1-1625408224.jpg" class="img-fluid" alt="">
                                    <img src="/images/ads-righthome-2-1628874547.jpg" class="img-fluid" alt="">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div class="thanbai">
        <div class="container mt-5"> 
            <div class="row mb-5 justify-content-center">
				<div class="col-lg-6 text-center">
					<h2 class="section-title text-center mb-3">Our Services
                    </h2> <hr>
					<p>Far far away, behind the word mountains, far from the countries Vokalia and Consonantia, there live the blind texts. Separated they live in Bookmarksgrove right at the coast of the Semantics, a large language ocean.</p>
				</div>
			</div> 
            <div class="row">  
                <!-- First Column: Image -->
                <div class="col-md-4">  
                    <div class="img-fluid">  
                        <img src="/images/ctsp.jpg"  class="d-block w-100 " alt="...">  
                    </div>
                </div>
                
                <!-- Second Column: Two Cards -->
                <div class="col-md-4">
                    <div class="card text-center p-3 mt-5">  
                        <i class="bi bi-house-door-fill" style="font-size: 2rem;"></i>  
                        <h5>Beautiful Condo</h5>  
                        <p>Even the all-powerful Pointing has no control about the blind texts.</p>  
                    </div>
                    <div class="card text-center p-3 mt-5">  
                        <i class="bi bi-envelope-fill" style="font-size: 2rem;"></i>  
                        <h5>Easy to Connect</h5>  
                        <p>Even the all-powerful Pointing has no control about the blind texts.</p>  
                    </div>
                </div>
    
                <!-- Third Column: Two More Cards -->
                <div class="col-md-4">
                    <div class="card text-center p-3 mt-5">  
                        <i class="bi bi-cup-hot" style="font-size: 2rem;"></i>  
                        <h5>Restaurants & Cafe</h5>  
                        <p>Even the all-powerful Pointing has no control about the blind texts.</p>  
                    </div>  
                    <div class="card text-center p-3 mt-5">  
                        <i class="bi bi-telephone-fill" style="font-size: 2rem;"></i>  
                        <h5>24/7 Support</h5>  
                        <p>Even the all-powerful Pointing has no control about the blind texts.</p>  
                    </div>
                </div>   
            </div>
            <div class="container text-center my-4 mt-5">
                <div class="row">
                    <div class="col">
                        <h2>9,313</h2>
                        <p>No. of Travels</p>
                    </div>
                    <div class="col">
                        <h2>8,492</h2>
                        <p>No. of Cities</p>
                    </div>
                    <div class="col">
                        <h2>100</h2>
                        <p>No. of Employees</p>
                    </div>
                    <div class="col">
                        <h2>120</h2>
                        <p>No. of Countries</p>
                    </div>
                </div>
            </div>
            <div class="container text-center my-4">
                <h2 class="section-title text-center mb-3" >Popular Destination</h2>
                <hr>
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
  </main>
</template>




