<template>
  <h1>The Movie Data Base Project</h1>
  <br />
  <div id="selection">
    <select id="option" v-model="name">
      <option value="299534">Avengers Endgame</option>
      <option value="299536">Avengers Infinity War</option>
      <option value="634649">Spider-Man No Way Home</option>
      <option value="324857">Spider-Man Into the Spider-Verse</option>
      <option value="140607">Star Wars The Force Awakens</option>
      <option value="1891">Star Wars The Empire Strikes Back</option>
      <option value="9615">The Fast and the Furious Tokyo Drift</option>
      <option value="337339">The Fast and the Furious The Fate of the Furious</option>
      <option value="566525">Shang-Chi and the Legend of the Ten Rings</option>
      <option value="14836">coraline</option>
    </select>
    <input type="button" @click="getmovie()" id="get" value="GET" />
  </div>
  <br />

  <br />
  <div id="descriptions">
    <h2 id="title"> {{ title }} </h2>
    <div id="overviewtitle">Overview:</div>
    <div id="overView"> {{ overview }} </div>
    <img :src="posterPath" id="idName" />
    <iframe id="idiframe" :src="trailer"></iframe>
    <p>Budget: {{ budget }} </p>
    <p>popularity: {{ popularity }}</p>
    <p>Average vote: {{ averagevote }} </p>
    <p>Vote Count: {{ votecount }} </p>
    <p>Original Language: {{ originallanguage }} </p>
    <p>Adult content: {{ adultcontent }} </p>
    <p>Release Date: {{ releasedate }} </p>
    <p>Revenue: {{ revenue }} </p>
    <p>Runtime: {{ runtime }} </p>

  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";
const name = ref(null);
let posterPath = ref(null);
let trailerPath = ref(null);
let title = ref("");
let overview = ref("");
let budget = ref("")
let popularity = ref("");
let trailer = ref("");
let averagevote = ref("");
let votecount = ref("");
let originallanguage = ref("");
let adultcontent = ref("");
let releasedate = ref("");
let revenue = ref("");
let runtime = ref("");

function getmovie() {
  let search = axios.get(`https://api.themoviedb.org/3/movie/${name.value}`, {
    params: {
      api_key: "e06cb446302dcf3a3cb1358720141aad",
      append_to_response: "videos",
    },
  });
  let searchResult = search.then((movieData) => {

    posterPath.value = `https://image.tmdb.org/t/p/w500/${movieData.data.poster_path}`
    trailer.value = "https://www.youtube.com/embed/" + (movieData.data.videos.results.filter((trailer) => trailer.type === "Trailer")).at(0).key;

    title.value = movieData.data.original_title; 
    overview.value = movieData.data.overview
    budget.value = movieData.data.budget
    popularity.value = movieData.data.popularity;
    averagevote.value = movieData.data.vote_average
    votecount.value = movieData.data.vote_count
    originallanguage.value = movieData.data.original_language
    adultcontent.value = movieData.data.adult
    releasedate.value = movieData.data.release_date
    revenue.value = movieData.data.revenue
    runtime.value = movieData.data.runtime
  });
}
</script>

<style scoped>
h1,
h2 {
  text-align: center;
  font-style: italic;
}

h2 {
  font-size: 26px;
}

p {
  font-size: 22px;
  position: relative;
  left: 5vw;
  margin: 44px;
}
 iframe {
  float: right;
  position: relative;
  height: 15vw;
  width: 30vw;
  right: 10vw;
  top: 9vw;

 }

 img {
  float: right;
  position: relative;
  width: 24vw;
 }

#overView {
  text-align: center;
  font-size: 18px;
  margin: 20px;
}

#selection {
  position: relative;
  left: 39.75vw;
}

#overviewtitle {
  text-align: center;
  font-size: 30px;
}
</style>
