<script>
  import Movie from './Movie.svelte'
  let value = ''
  let response = []

  const handleInput = (e) => {
    value = e.target.value
  }

  $: if(value.length > 5) {
    getMovies()
  }

  async function getMovies() {
    const url = await fetch(`https://www.omdbapi.com/?s=${value}&apikey=422350ff`)
    const data = await url.json()
    response = data.Search || []

    if (url.ok) {
			return response
		} else {
			throw new Error('Hubo un error al cargar las peliculas')
		}
  }
</script>

<input type="text" value={value} on:input={handleInput}>

{#await response}
  <p>Cargando pelis 🎉</p>
{:then movies}
  {#each movies as {Title, Poster, Year}, index}
    <Movie index={index} title={Title} poster={Poster} year={Year}  />
  {:else}
    <p>No hay peliculas...</p>
  {/each}
{:catch error}
  <p>😫 Error al cargar las peliculas</p>
{/await}


