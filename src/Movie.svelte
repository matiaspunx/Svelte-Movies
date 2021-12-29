<script>
  export let index, poster, title, year;
</script>

<article id={`id${index}`}>
  <img src={poster} alt={title}>
  <div>
    <h3>{title}</h3>
    <p>{year}</p>
    {#if 2020 - year < 5}
      <span>🆕</span>
    {/if}
  </div>
</article>

<style>
  article {
    display: flex;
  }
  article img {
    margin-right: 1rem;
    width: 200px;
    object-fit: cover;
  }
</style>