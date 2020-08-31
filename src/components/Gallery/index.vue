<template>
  <section class="container py-5">
    <h4 class="title-app">{{state.name}}</h4>
    <!-- <input v-model="state.name" type="text" /> -->
    <p class="text-muted">{{favoriteCount}} Favorited Photo</p>
    <div class="row mt-4">
      <div class="col-4" v-for="(photo, index) in state.photos" :key="index">
        <div class="card mb-4">
          <img class="card-img-top" :src="photo.urls.small" alt="Card image cap">
          <div class="card-body d-flex flex-column justify-content-between">
            <div>
              <h5 class="card-title">{{photo.user.first_name}}</h5> 
              <p class="card-text text-muted">{{photo.alt_description}}</p>
            </div>
            <div>
              <button class="btn btn-light" :class="{'text-danger': photo.isFavorite}" v-on:click="addToFavorite(photo)">❤ Favorite</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { reactive, onMounted, computed, watch } from 'vue'; 
  export default {
    name: "Gallery",
    // props: {
    //   title: String,
    // },

    setup() {
      console.log('setup dijalankan')

      // dinamic data
      const state = reactive({
        name: "My Gallery",
        photos: []
      })

      // --- lifecycle ---
      onMounted( async ()=>{
        console.log('mounted dijalankan')

        const response = await fetch('https://api.unsplash.com/photos/?client_id=MWofT621uSFp8FGPPqx5wb5XSxhPtWFlJtETA2dHLo8&orientation=landscape&query=office&')
        const data = await response.json()
        data.map(item => item.isFavorite = false)
        state.photos = data

        console.log(data)

      })

      function addToFavorite (photo) {
        photo.isFavorite = !photo.isFavorite
        
        console.log('terpanggil', photo)
      }

      const favoriteCount = computed(()=> state.photos.filter(photo => photo.isFavorite).length)

      watch(()=> state.name, (newValue, oldValue)=> {
        console.log(newValue, 'ini new value')
        console.log(oldValue, 'ini old value')
      })
      
      return {
        state,
        addToFavorite,
        favoriteCount
      };
    }
  }
</script>

<style scoped>
  .title-app{
    font-weight: 500;
  }
  .card {
    border: none;
    border-radius: 10px;
    -webkit-box-shadow: 2px 2px 15px 0px rgba(0,0,0,0.45);
    -moz-box-shadow: 2px 2px 15px 0px rgba(0,0,0,0.45);
    box-shadow: 2px 2px 15px 0px rgba(0,0,0,0.45);
    min-height: 421px;
  }
  .card .card-img-top{
    height: 230px;
    object-fit: cover;
    object-position: center;
    border-radius: 10px 10px 0 0;
  }
</style>
