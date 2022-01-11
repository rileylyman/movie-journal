<script>
  import MovieInput from "./MovieInput.svelte";
  import MovieList from "./MovieList.svelte";
  import Search from "./Search.svelte";

  const getMovies = () =>
    localStorage.getItem("movies")
      ? JSON.parse(localStorage.getItem("movies"))
      : [];

  let movies = getMovies();

  const onMovieSubmitted = (event) => {
    movies = [event.detail.movie, ...movies];
    localStorage.setItem("movies", JSON.stringify(movies));
  };

  const updateSearchTerm = (term) => {
    movies = getMovies().filter((m) =>
      m.title.toLowerCase().includes(term.toLowerCase())
    );
  };

  const clearSearchTerm = () => {
    movies = getMovies();
  };
</script>

<div class="main">
  <h1>Movie Journal</h1>

  <Search
    on:clear-search={clearSearchTerm}
    on:search={(e) => updateSearchTerm(e.detail)}
  />
  <MovieInput on:movie-submitted={onMovieSubmitted} />
  <MovieList {movies} />
</div>

<style>
  .main {
    width: 500px;
    max-width: 100%;
    padding: 1em;
    margin: auto;
    text-align: center;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
</style>
