
<template>
  <h1> The Movie Data Base Project</h1>
  <br>
  <div id="selection">
    <select id="option" v-model="name">
      <option value="Avengers Endgame">Avengers Endgame</option>
      <option value="Avengers Infinity War">Avengers Infinity War</option>
      <option value="Spider-Man No Way Home">Spider-Man No Way Home</option>
      <option value="Spider-Man Into the Spider-Verse">Spider-Man Into the Spider-Verse</option>
      <option value="Star Wars The Force Awakens">Star Wars The Force Awakens</option>
      <option value="Star Wars The Empire Strikes Back">Star Wars The Empire Strikes Back</option>
      <option value="The Fast and the Furious Tokyo Drift">The Fast and the Furious Tokyo Drift</option>
      <option value="The Fast and the Furious The Fate of the Furious">The Fast and the Furious The Fate of the Furious
      </option>
      <option value="Shang-Chi and the Legend of the Ten Rings">Shang-Chi and the Legend of the Ten Rings</option>
      <option value="coraline">coraline</option>
    </select>
    <input type="button" @click="info" id="get" value="GET">
  </div>
  <br>

  <br>
  <div id="descriptions" v-if="update">
    <h2 id="title">{{ update.original_title }}</h2>
    <div id="overviewtitle"> Overview: </div>
    <div id="overview">{{ update.overview }}</div>
    <p> Budget: {{ Budget }}</p>
    <p> popularity: {{ update.popularity }}</p>
    <p> Average vote: {{ update.vote_average }}</p>
    <p> Vote Count: {{ update.vote_count }}</p>
    <p> Original Language: {{ update.original_language }}</p>
    <p> Adult content: {{ update.adult }}</p>
    <p> Release Date: {{ update.release_date }}</p>
    <p> Revenue: {{ update.revenue }}</p>
    <p> Runtime: {{ update.runtime }}</p>


    <img :src=posterPath id="idName">
    <iframe id="idiframe" :src="trailerPath"></iframe>
  </div>

</template>

<script setup>
import { V_ON_WITH_KEYS } from '@vue/compiler-dom';
import axios from 'axios';
import { ref } from "vue";

const name = ref(null);
const update = ref(null);

let posterPath = ref(null);
let trailerPath = ref(null);

let Budget = ref(null);
const popularity = ref(null);
const Averagevote = ref(null);
const VoteCount = ref(null);
const OriginalLanguage = ref(null);
const Adultcontent = ref(null);
const ReleaseDate = ref(null);
const Revenue= ref(null);
const Runtime= ref(null);

const info = async () => {
  const moviename = name.value;
  let searchUpdate = axios.get("https://api.themoviedb.org/3/search/movie", {
    params: {
      api_key: "a59d2813d99007b086e055a41d8a036f",
      include_adult: "false",
      query: moviename,
    }
  });
  

  let newUpdateposter = searchUpdate.then((movieposters) => {
    update.value = movieposters.data.results[0];
    posterPath = "https://image.tmdb.org/t/p/w500/" + update.value.poster_path;
    //trailerPath = "https://www.youtube.com/embed/" + (movieposters.data.results[0].videos.results.filter((trailer) => trailer.type === "Trailer")).at(0).key;
    Budget = update.value.data.budget;
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
  font-size: 32px;
}

p {
  font-size: 24px;
  position: relative;
  left: 7vw;
  margin: 44px;
}

#a {
  text-align: center;
  font-size: 17.25px;
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

