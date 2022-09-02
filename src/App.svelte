<script>
  import Character from "./lib/Character.svelte";
  let characters = [];
  let pagina = 1;

  async function loadCharacters() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + pagina
    );
    const data = await response.json();
    console.log(data);
    characters = data.results;
  }
  loadCharacters();

  function siguientePagina() {
    pagina++;
    loadCharacters();
  }

  function anteriorPagina() {
    pagina--;
    loadCharacters();
  }
</script>

<h1 class="title">Rick and Morty Whith SVELTE</h1>

<div class="container">
  <div class="btns">
    <button class="btn" on:click={anteriorPagina} disabled={pagina === 1}>Anterior</button>
    <button class="btn" on:click={siguientePagina}>Siguiente</button>
  </div>
  <div class="grid">
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>
</div>
