<script>
  import { createEventDispatcher } from "svelte";

  let dispatch = createEventDispatcher();

  let title = "";
  let rating = 1;

  const submitMovie = (_) => {
    dispatch("movie-submitted", {
      movie: { title: title, rating: rating },
    });
    title = "";
    rating = 1;
  };
</script>

<div class="main">
  <input placeholder="Movie Title" type="text" bind:value={title} />

  <select bind:value={rating}>
    <option value={1}> 1 </option>
    <option value={2}> 2 </option>
    <option value={3}> 3 </option>
    <option value={4}> 4 </option>
    <option value={5}> 5 </option>
  </select>

  <button disabled={!title} on:click={submitMovie}>Submit</button>
</div>

<style>
  .main {
    width: 100%;
    display: flex;
  }

  .main input {
    flex: 1;
  }

  .main select {
    width: 75px;
    margin-left: 10px;
  }

  .main button {
    width: 75px;
    margin-left: 10px;
  }
</style>
