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
  <div id="descriptions" v-if="update">
    <h2 id="title">{{ update.original_title }}</h2>
    <div id="overviewtitle">Overview:</div>
    <div id="overview">{{ update.overview }}</div>
    <p>Budget: {{ update.budget }}</p>
    <p>popularity: {{ update.popularity }}</p>
    <p>Average vote: {{ update.vote_average }}</p>
    <p>Vote Count: {{ update.vote_count }}</p>
    <p>Original Language: {{ update.original_language }}</p>
    <p>Adult content: {{ update.adult }}</p>
    <p>Release Date: {{ update.release_date }}</p>
    <p>Revenue: {{ update.revenue }}</p>
    <p>Runtime: {{ update.runtime }}</p>

    <img :src="posterPath" id="idName" />
    <iframe id="idiframe" :src="trailerPath"></iframe>
  </div>
</template>

<script setup>
import axios from "axios";
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
const Revenue = ref(null);
const Runtime = ref(null);
let searchUpdate;

function getmovie() {
  const info = async () => {
    const moviename = name.value;
    searchUpdate = axios.get(`https://api.themoviedb.org/3/movie/${moviename}`, {
      params: {
        api_key: "a59d2813d99007b086e055a41d8a036f",
        include_adult: "false",
      },
    });
  };
  let newUpdateposter = searchUpdate.then((movieData) => {
    // update.value = movieposters.data;
    // posterPath = "https://image.tmdb.org/t/p/w500/" + update.value.poster_path;
    // trailerPath =
    //   "https://www.youtube.com/embed/" +
    //   movieposters.data.results[0].videos.results
    //     .filter((trailer) => trailer.type === "Trailer")
    //     .at(0).key;
    // Budget = update.value.budget;
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
