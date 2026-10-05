<script setup lang="ts">
import { RouterLink, RouterView, useRouter } from 'vue-router';
import { ref, computed } from 'vue';
import { isAuthenticated, userLogout, userRole } from './stores/user';

const router = useRouter();
const keyword = ref ('');

const handleSearch = ()=>{
  if(keyword.value){
    // console.log(keyword.value)
    router.push({
      path: 'timkiem',
      query: {tukhoa: keyword.value}
    });
  }
}

const handelLogout=() => {
    userLogout();
    router.push('/login')
}
// Computed property để kiểm tra role
const isAdmin = computed(() => userRole.value === 'admin');

</script>

<template>
<div>
  <header>
    <div class="container" style="background-color: #6998AB;">
    <nav style="background-color: #6998AB;" class="navbar navbar-expand-lg navbar-light bg-light">  
      <div class="container-fluid">  
        <RouterLink class="navbar-brand" to="/">Rubik</RouterLink>  
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">  
          <span class="navbar-toggler-icon"></span>  
        </button>  
        <div class="collapse navbar-collapse" id="navbarNav">  
          <ul class="navbar-nav">  
            <li class="nav-item">  
              <RouterLink class="nav-link active" aria-current="page" to="/">Home</RouterLink>  
            </li>  
            <li class="nav-item">  
              <RouterLink class="nav-link" to="/services">Sản Phẩm</RouterLink>  
            </li>  
            <li class="nav-item">  
              <RouterLink class="nav-link" to="/services/:id">Sản phẩm chi tiết</RouterLink>  
            </li>  
            <li class="nav-item">  
              <RouterLink class="nav-link" to="/contact">Liên Hệ</RouterLink>  
            </li>
            <li class="nav-item">  
              <RouterLink class="nav-link" v-if="isAuthenticated && isAdmin" to="/productManagement"> Products Management</RouterLink>
            </li><li class="nav-item">  
              <RouterLink  v-if="isAuthenticated && isAdmin" class="nav-link" to="/categoriesManagement">Categories Management</RouterLink>
            </li>  
          </ul> 
            <div class="ms-auto d-flex">
              <div class="input-group me-2">
              <input v-model="keyword" @keyup.enter="handleSearch" type="text" placeholder="Tim kiem" class="form-control">
              <button @click="handleSearch" class="btn btn-danger"><i class="bi bi-search-heart fs-6"></i></button>
            </div>
            <div class="me-2">
              <RouterLink class="nav-link" to="/shopping-cart" > <button  class="btn btn-primary"  ><i class="bi bi-cart-plus-fill"></i> </button>  </RouterLink>
            </div>
            <div class="dropdown ">  
                <a class="btn dropdown-toggle btn-primary" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">  
                  <i class="bi bi-person-circle fs-6"></i> 
                </a>  
                <ul class="dropdown-menu"> 
                  <li><RouterLink v-if="!isAuthenticated" class="dropdown-item" to="/login">Login</RouterLink></li>    
                  <li><RouterLink v-if="!isAuthenticated" class="dropdown-item" to="/signup">Create new account</RouterLink></li>
                  <li><RouterLink v-if="!isAuthenticated" class="dropdown-item" to="/forgot-password">Forgotten account</RouterLink></li>  
                  <li><RouterLink v-if="isAuthenticated" class="dropdown-item" to="/profile">Profile</RouterLink></li>
                  <li><RouterLink v-if="isAuthenticated && isAdmin" class="dropdown-item" to="/productManagement"> Products Management</RouterLink></li>
                  <li><RouterLink v-if="isAuthenticated && isAdmin" class="dropdown-item" to="/categoriesManagement">Categories Management</RouterLink></li>
                  <li><RouterLink v-if="isAuthenticated" class="dropdown-item" to="/profile">Change Pass</RouterLink></li>
                  <li class="text-center"><button v-if="isAuthenticated" @click="handelLogout" class="btn btn-danger">Logout</button></li>
                </ul>  
            </div>
            </div>
        </div>  
      </div>  
    </nav>
  </div>
  </header>
  <RouterView />
  <footer>
    <div class="site-footer mt-5">  
        <div class="inner first">  
            <div class="container">  
                <div class="row">  
                    <div class="col-md-6 col-lg-4">  
                        <div class="widget">  
                            <h3 class="heading">About Tour</h3>  
                            <p>Far far away, behind the word mountains, far from the countries Vokalia and Consonantia, there live the blind texts.</p>  
                        </div>  
                        <div class="widget">  
                            <ul class="list-unstyled social">  
                                <li><a href="#"><i class="fab fa-twitter"></i></a></li>  
                                <li><a href="#"><i class="fab fa-instagram"></i></a></li>  
                                <li><a href="#"><i class="fab fa-facebook-f"></i></a></li>  
                                <li><a href="#"><i class="fab fa-linkedin-in"></i></a></li>  
                                <li><a href="#"><i class="fab fa-dribbble"></i></a></li>  
                                <li><a href="#"><i class="fab fa-pinterest"></i></a></li>  
                                <li><a href="#"><i class="fab fa-apple"></i></a></li>  
                                <li><a href="#"><i class="fab fa-google"></i></a></li>  
                            </ul>  
                        </div>  
                    </div>  
                    <div class="col-md-6 col-lg-2 pl-lg-5">  
                        <div class="widget">  
                            <h3 class="heading">Pages</h3>  
                            <ul class="links list-unstyled">  
                                <li><a href="#">Blog</a></li>  
                                <li><a href="#">About</a></li>  
                                <li><a href="#">Contact</a></li>  
                            </ul>  
                        </div>  
                    </div>  
                    <div class="col-md-6 col-lg-2">  
                        <div class="widget">  
                            <h3 class="heading">Resources</h3>  
                            <ul class="links list-unstyled">  
                                <li><a href="#">Blog</a></li>  
                                <li><a href="#">About</a></li>  
                                <li><a href="#">Contact</a></li>  
                            </ul>  
                        </div>  
                    </div>  
                    <div class="col-md-6 col-lg-4">  
                        <div class="widget">  
                            <h3 class="heading">Contact</h3>  
                            <ul class="list-unstyled quick-info links">  
                                <li class="email"><a href="mailto:mail@example.com"><i class="fas fa-envelope"></i> mail@example.com</a></li>  
                                <li class="phone"><a href="tel:+12222123819"><i class="fas fa-phone"></i> +1 222 212 3819</a></li>  
                                <li class="address"><i class="fas fa-map-marker-alt"></i> 43 Raymouth Rd. Baltemoer, London 3910</li>  
                            </ul>  
                        </div>  
                    </div>  
                </div>  
            </div>  
        </div>  

    </div> 
</footer>
</div>
</template>




