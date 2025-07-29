

<template>
  <div class="form">
    <h1 class="logoTitle">MOVIE SEARCH</h1>
    <div class="inputForm">
      <input @keyup.enter="getData" v-model="movieName" type="text" name="movieNameInput" placeholder="Введите название фильма...">
      <button @click="getData"> ↪ </button>
    </div>
    <p> {{errorMsg}}</p>


  </div>

  <div class="sortArea">
    <p>sort by: </p>

    <button class="yearBtn">year</button>
    <button class="ratingBtn">rating</button>
    <button class="lengthBtn">length</button>

  </div>

  <div class="main">
    <div class="movieCardsArea">
      <div class="movieCards" v-for="element in data" :key="element.filmId">
        <MovieCard :movie="element"></MovieCard>

      </div>
    </div>
  </div>


</template>

<style scoped>


.form {
  display: flex;
  flex-direction: column;

  align-items: center;
}

.logoTitle{
  color: #FAEFD9;
  font-family: Ebrima;
  font-weight: lighter;
  font-size: 32px;
  margin: 24px;
}

.form input{
  padding: 15px;
  border: 0px;
  background-color: #FAEFD9;
  color: black;
  outline: none;
  width: 250px;
  height: 36px;
  font-size: 20px;
  border-radius: 10px;
}

.form button{
  padding: 25px;
  border: 1px solid #FAEFD9;
  border-radius: 10px;
  margin: 10px;
  color: #FAEFD9;
  transition: background-color revert-layer 100ms 0ms;
}
.form button:hover{
  background-color: #FAEFD9;
  color: #1D1C25;

}

p{
  color: #FAEFD9;
  font-size: 20px;
  margin-top: 20px;
}

.sortArea {
  display: flex;
  flex-direction: row;
  align-items: center;

}

.sortArea p{
  margin-left: 10vw;
  font-size: 30px;
}

.sortArea button {
  margin-top: 20px;
  margin-left: 30px;
  border: 2px solid #FAEFD9;
  padding: 15px;
  border-radius: 35px;
  color: #FAEFD9;
  width: 100px;
  font-size: 20px;
}


.movieCardsArea {

  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 100px;
  margin: 7%;



}

</style>

<script lang="ts">



  import axios from 'axios'
  import MovieCard from "@/components/movieCard.vue";

  export default {
    components: {MovieCard},
    data(){
      return{
        movieName: "",
        errorMsg: "",
        isLoading: false,
        data: [],

      }
    },
    methods:{
      async getData() {
        try {
          if (!this.movieName.trim()) {
            this.errorMsg = "Введите название фильма";
            this.data = [];
            return;
          }


          this.errorMsg = "";


          const apiKey = '0f5649c9-1915-4a88-a844-fd3e72b6d698';//process.env.VUE_APP_KINOPOISK_API_KEY;
          const apiUrl = 'https://kinopoiskapiunofficial.tech/api/v2.1/films/search-by-keyword'//process.env.VUE_APP_API_URL;

          this.isLoading = true;

          const response = await axios.get(
              apiUrl,
              {
                params: {
                  keyword: this.movieName,
                  page: 1,
                },
                headers: {
                  'X-API-KEY': apiKey,
                  'Content-Type': 'application/json',
                }
              }
          );


          this.data = response.data.films || [];



          if (this.data.length === 0) {
            this.errorMsg = "Фильмы не найдены";
          }

        } catch (error) {

          console.error("Ошибка при запросе:", error);
          this.errorMsg = "Произошла ошибка при загрузке данных";
          this.data = [];
        } finally {
          this.isLoading = false;

        }
      }
    }
  }
</script>