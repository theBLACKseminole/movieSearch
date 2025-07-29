<script lang="ts">
 import * as url from "node:url";

 export default {
   computed: {
     imageStyle() {
       return {
         backgroundImage: `url('${this.movie.posterUrl}')`,
         width: '400px',
         height: '600px',
         backgroundSize: 'cover',
         backgroundPosition: 'center',
         backgroundRepeat: 'no-repeat'
       }
     }
   },
   props: {
     movie: {
       type: Object,
       required: true
     }
   },
   data() {
     return {

     };
   }
 }
</script>

<template>
  <div class="card">
    <div class="card-bg" :style="imageStyle"></div>
    <div class="movieInfoPreview">
      <div class="infoHeader">
        <img src="@/assets/ratingIcon.svg.svg" alt="ratingIcon">
        <label>{{movie.rating}}</label>
      </div>
      
      <div class="infoMain">
        <label>{{movie.nameEn}}</label>
        <label class="ruLabel">{{movie.nameRu}}</label>
      </div>
      <div class="infoFooter">
        <label>◷{{movie.filmLength}}</label>
        <label>{{movie.year}}</label>
      </div>
    </div>
  </div>
</template>

<style scoped>
  * {
    background-color: transparent;
  }

  .movieInfoPreview{
    width: 400px;
    height: 600px;
    display: flex;
    flex-direction: column;
    opacity: 0;
    transition: opacity 50ms 0ms;

  }
  .infoHeader {

    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    margin-left: 20px;
    margin-top: 10px;
    z-index: 2;
    width: 60px;
    height: 30px;
    padding: 10px;
    align-items: center;
    gap: 10px;
    background-color: #1D1C25;
    color: #FAEFD9;
    border-radius: 10px;
  }
  .infoMain {

    display: flex;
    flex-direction: column;
    font-size: 35px;

    text-shadow: 1px 1px 4px rgba(0, 0, 0, 1);

    text-transform: uppercase;
    font-family: Ebrima;
    font-weight: lighter;
    text-align: center;
    margin-top: 40%;
    justify-content: center;



    align-items: center;
    gap: 10px;

    color: #FAEFD9;
    border-radius: 10px;
    z-index: 2;
  }
  .ruLabel {
    font-size: 25px;

    color: #e4d4b6;
  }
  .infoFooter {
    z-index: 2;
  }

  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

  }
  .card-bg {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;


    width: 400px;
    height: 600px;
    border-radius: 20px;
    overflow: hidden;


    transition: filter linear 500ms 0ms;
    transition: transform linear 200ms 0ms;
    z-index: 1;

  }

  .card:hover .card-bg {
    filter: grayscale(80) blur(5px);
    transform: scale(105%);
  }

  .card:hover .movieInfoPreview {
    opacity: 100;
  }


</style>