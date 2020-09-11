<style>
  .details {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    width: 100%;
    max-width: 900px;
    margin: 0 auto;
    min-height: 100vh;
    height: auto;
    top: -10px;
    overflow: hidden;
    padding: 0;
    border-radius: 1em;
    z-index: 9;
    background-color: var(--color-white);
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  }

  .breadcumb {
    display: flex;
    justify-content: start;
    align-items: center;
    color: var(--color-white);
    margin: 0;
    padding: 0;
    width: 100%;
    height: 40px;
    position: absolute;
    background-color: #39393955;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    overflow: hidden;
  }

  .breadcumb .btn-back {
    background-color: transparent;
    border: none;
    color: var(--color-white);
    margin: 0 0 0 26px;
    cursor: pointer;
  }

  .backdrop {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 300px;
    display: flex;
    justify-content: start;
    align-items: start;
    overflow: hidden;
  }
  .backdrop img {
    width: 100%;
  }

  .header {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: flex-start;
    position: relative;
    width: 100%;
    margin-bottom: 20px;
  }

  .header .poster {
    position: absolute;
    top: -120px;
    left: 40px;
    margin: 0;
  }

  .header .poster img {
    border-radius: 0.5rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.5);
  }
  /* USAR GRID LAYOUT*/
  .header .info {
    flex-direction: column;
    width: 100%;
    margin: 0 0 0 220px;
  }

  .header .info .title {
    margin: 20px 0 0 0;
    text-transform: uppercase;
  }

  .header .info .category {
    width: 100%;
    margin: 10px 0;
  }

  .overview {
    margin: 20px 40px;
    font-size: 1rem;
    line-height: 20px;
  }

</style>

<script lang="ts">
  import { onMount ,onDestroy, createEventDispatcher } from 'svelte';
  import image from '../settings/image';

  import PosterListCard from '../components/PosterListCard.svelte';

  export let details;
  let dispatch = createEventDispatcher();
  const genres = details && details.genres && details.genres.map(genre => genre.name).join(' | ');

  const handleLoadDetails = (id) => dispatch('handleLoadDetails', id);

  onMount(() => {
    window.scrollTo(0,0);
  });

  onDestroy(() => {
    details = null;
  });
</script>

<article class="details">
  <nav aria-label="breadcrumb" class="breadcumb">
    <button type="button" class="btn-back" on:click={() => dispatch('handleBackHome')}>Home</button>
  </nav>
  <figure class="backdrop">
    <img
      src={`${image.secure_base_url}${image.backdrop_sizes.w780}${details.backdrop_path}`}
      alt={details.title}
    />
  </figure>
  <header class="header">
    <figure class="poster">
      <img
        src={`${image.secure_base_url}${image.poster_sizes.w154}${details.poster_path}`}
        alt={details.title}
      />
    </figure>
    <div class="info">
      <h1 class="title">{details.title}</h1>
      <p class="category">{genres}</p>
    </div>
  </header>
  <p class="overview">{details.overview}</p>
  <hr />
  <PosterListCard title="Recommendations" on:handleLoadDetails={handleLoadDetails} />
</article>
