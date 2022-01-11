<script>
  import { createEventDispatcher } from "svelte";

  let value = "";
  let dispatch = createEventDispatcher();

  const search = () => {
    if (value) {
      dispatch("search", value);
    } else {
      dispatch("clear-search", null);
    }
  };
</script>

<input placeholder="Search Your Movies" bind:value on:keyup={search} />

<style>
  input {
    width: 100%;
  }
</style>
