<script setup>
import axios from 'axios';

function myFunction() {

document.getElementById("idName").remove()
document.getElementById("idiframe").remove()


  let response = axios.get("https://api.themoviedb.org/3/search/movie", {
params: {
  api_key: "a59d2813d99007b086e055a41d8a036f",
  include_adult: "false",
  query: document.getElementById('option').value,
}
});

response = response.then((moviesData) => {
for (let movie of moviesData.data.results) {   
  axios.get(`https://api.themoviedb.org/3/movie/${movie.id}`, {
    params: {
      api_key: "a59d2813d99007b086e055a41d8a036f",
      append_to_response: "videos", }})
    .then((get) => {
    const img = document.createElement('img');
    img.id="idName"
    const iframe = document.createElement('iframe');
    iframe.id="idiframe"
    const trailers = get.data.videos.results.filter((trailer) => trailer.type === "Trailer");
    iframe.src = `https://www.youtube.com/embed/${trailers.at(0).key}`
    img.src = `https://image.tmdb.org/t/p/w500${movie.poster_path}`;
    document.body.append(img);
    document.body.append(iframe);



  document.getElementById('title').innerHTML = get.data.original_title
  document.getElementById('a').innerHTML = get.data.overview
  document.getElementById('b').innerHTML = get.data.budget
  document.getElementById('c').innerHTML = get.data.popularity
  document.getElementById('d').innerHTML = get.data.vote_average
  document.getElementById('e').innerHTML = get.data.vote_count
  document.getElementById('f').innerHTML = get.data.original_language
  document.getElementById('g').innerHTML = get.data.adult
  document.getElementById('h').innerHTML = get.data.release_date
  document.getElementById('i').innerHTML = get.data.revenue
  document.getElementById('j').innerHTML = get.data.runtime

  

})}})}
</script>

<template>
    <h1> The Movie Data Base Project</h1>
        <br>
        <div id="selection">
            <select id="option">
            <option value="Avengers Endgame">Avengers Endgame</option>
            <option value="Avengers Infinity War">Avengers Infinity War</option>
            <option value="Spider-Man No Way Home">Spider-Man No Way Home</option>
            <option value="Spider-Man Into the Spider-Verse">Spider-Man Into the Spider-Verse</option>
            <option value="Star Wars The Force Awakens">Star Wars The Force Awakens</option>
            <option value="Star Wars The Empire Strikes Back">Star Wars The Empire Strikes Back</option>
            <option value="The Fast and the Furious Tokyo Drift">The Fast and the Furious Tokyo Drift</option>
            <option value="The Fast and the Furious The Fate of the Furious">The Fast and the Furious The Fate of the Furious</option>
            <option value="Shang-Chi and the Legend of the Ten Rings">Shang-Chi and the Legend of the Ten Rings</option>
            <option value="coraline">coraline</option>
            </select>
            <input type="button" @click= "myFunction()" id="get" value="GET">  
        </div>
        <br>

<br>
<div id="descriptions">
    <h2 id="title"></h2>
    <p> Overview: </p>
    <div id="a"></div>
    <br>
    <dl id="list">
<dt id="a1"></dt>
    <br>
    <dt> Budget:</dt>
    <br>
    <div id="b"></div>
    <br>
    <dt> Popularity: </dt>
    <br>
    <div id="c"></div>
    <br>
    <dt> Average votes:</dt>
    <br>
    <div id="d"></div>
    <br>
    <dt> Amount of votes:</dt>
    <br>
    <div id="e"></div>
    <br>
    <dt> original language:</dt>
    <br>
    <div id="f"></div>
    <br>
    <dt> Adult count:</dt>
    <br>
    <div id="g"></div>
    <br>
    <dt> Release date:</dt>
    <br>
    <div id="h"></div>
    <br>
    <dt> Revenue:</dt>
    <br>
    <div id="i"></div>
    <br>
    <dt> Runtime:</dt>
    <br>
    <div id="j"></div>
</dl>
<img id="idName">
<iframe id="idiframe"></iframe>

</div>
</template>
