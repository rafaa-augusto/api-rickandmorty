<script setup>
    import { onMounted, ref } from 'vue';
    
    let personagens = ref([]);
    let termoBusca = ref('');
    
    function buscarPersonagens() {
      fetch(`https://rickandmortyapi.com/api/character/?name=${termoBusca.value}`)
        .then(response => response.json())
        .then(response => {
          personagens.value = response.results;
        });
    }
    
    onMounted(() => {
      fetch("https://rickandmortyapi.com/api/character")
        .then(response => response.json())
        .then(response => {
          personagens.value = response.results;
        });
    });
</script>


<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark border-bottom bordder-body">
    <div class="container-fluid">
      <router-link class="navbar-brand" to="/"><img src="/src/assets/image/portal-rickandomorty-removebg-preview.png" alt="" style="height: 50px;"></router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">About</router-link>
          </li>
        </ul>
        <form class="d-flex" @submit.prevent="buscarPersonagens">
          <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" v-model="termoBusca">
          <button class="btn btn-outline-success" type="submit">Search</button>
        </form>
      </div>
    </div>
  </nav>

  <div class="container">
    <div class="row">
      <div class="col-md-6" >
        <img src="/src/assets/image/Rick-And-Morty-Png-File-Rick-E-Morty-Logo-Png_-Transparent-Png-vhv-removebg-preview.png" alt="" class="logo-rickandmorty" >
      </div>
      <div class="col-md-6">
      </div>
    </div>
  </div>


  <div class="cards">
    <div class="card" v-for="personagem in personagens" :key="personagem.id">
      <img class="card-img-top" :src="personagem.image" :alt="personagem.name">
      <div class="card-body card-body ">
        <h5 class="card-title poetsen-one-regular d-flex justify-content-center align-items-center ">{{ personagem.name }}</h5>
        <p class="card-text poetsen-one-regular">Status: {{ personagem.status }}</p>
        <p class="card-text poetsen-one-regular">Espécie: {{ personagem.species }}</p>
        <p class="card-text poetsen-one-regular">Gênero: {{ personagem.gender }}</p>
        <p class="card-text poetsen-one-regular">Localização: {{ personagem.location.name }}</p>
      </div>
    </div>
  </div>


<footer>


</footer>



</template>


<style scoped>

.poetsen-one-regular {
  font-family: "Poetsen One", sans-serif;
  font-weight: 400;
  font-style: normal;
}



.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.card {
  width: 18rem;
  margin-bottom: 20px;
  background-color: rgba(112, 236, 10, 0.801) !important;
}

.card img{
  width: 85%;
  margin-left: 22px;
  margin-top: 5px;
  border-radius: 10px;
} 

.logo-rickandmorty{
  margin-left: 170px;
}

.card p{
  margin: 5px;
}

.card h5{
  margin-right:  20px;
}

</style>
