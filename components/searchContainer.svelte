<script>
  import { onMount } from 'svelte'
import { each } from 'svelte/internal';

  let returnedList = [];
  let query = '';
  let searchResults = [];

  async function handleQuery() {
    query = searchMovie.value
    const response = await fetch(`https://imdb-api.com/en/API/SearchMovie/--key goes here--/${query}`)
    returnedList = await response.json()
    searchResults = returnedList.results;
    console.log(searchResults) 
         
  }
  

</script>

<div class='searchContainer'>
  <label for="searchMovie">Enter a movie to search for</label>
  <input type="text" name="searchMovie" id="searchMovie">
  <button on:click={handleQuery}>Search</button>
  <h1>the movie that will be searched is: {query}</h1>
  {#each searchResults as returnedItem (returnedItem.id)}
  <div class="movieContainer">
    <h1>{returnedItem.title}</h1>
    <img class='movieImg' src={returnedItem.image} alt="" srcset="">
    <hr>
  </div>  
  
  {/each}
</div>

<style>
  .searchContainer{
    color: black;
  }
  .movieImg{
    max-width: 15rem;
    max-height: 25rem;
  }
</style>