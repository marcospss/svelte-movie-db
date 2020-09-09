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

  .backdrop {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 300px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
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
    padding: 10px;
    margin: 10px 0 10px 220px;
  }

  .header .info .title {
    margin: 0;
  }

  .header .info .category {
    width: 100%;
    margin: 10px 0;
    font-weight: bold;
  }

  .header .info .runtime {
    margin: 0;
    font-weight: bold;
  }

  .overview {
    margin: 20px 40px;
    font-size: 1rem;
    line-height: 20px;
  }

</style>

<script lang="ts">
  import { onDestroy, createEventDispatcher } from 'svelte';
  import image from '../settings/image';

  export let details = {
    adult: false,
    backdrop_path: '/xl5oCFLVMo4d4Pgxvrf8Jmc2IlA.jpg',
    belongs_to_collection: null,
    budget: 200000000,
    genres: [
      { id: 18, name: 'Drama' },
      { id: 28, name: 'Action' },
      { id: 10752, name: 'War' },
      { id: 14, name: 'Fantasy' },
      { id: 12, name: 'Adventure' },
    ],
    homepage: 'https://movies.disney.com/mulan-2020',
    id: 337401,
    imdb_id: 'tt4566758',
    original_language: 'en',
    original_title: 'Mulan',
    overview:
      'When the Emperor of China issues a decree that one man per family must serve in the Imperial Chinese Army to defend the country from Huns, Hua Mulan, the eldest daughter of an honored warrior, steps in to take the place of her ailing father. She is spirited, determined and quick on her feet. Disguised as a man by the name of Hua Jun, she is tested every step of the way and must harness her innermost strength and embrace her true potential.',
    popularity: 1180.813,
    poster_path: '/aKx1ARwG55zZ0GpRvU2WrGrCG9o.jpg',
    production_companies: [
      {
        id: 2,
        logo_path: '/wdrCwmRnLFJhEoH8GSfymY85KHT.png',
        name: 'Walt Disney Pictures',
        origin_country: 'US',
      },
      {
        id: 14714,
        logo_path: '/oQHaOZEnPzlJACVTisV0FICrS82.png',
        name: 'China Film Group Corporation',
        origin_country: 'CN',
      },
      {
        id: 103698,
        logo_path: '/qS01bSMe274ecTdrgyO3BBvzfKK.png',
        name: 'Good Fear',
        origin_country: 'US',
      },
      { id: 89254, logo_path: null, name: 'Jason T. Reed Productions', origin_country: 'US' },
      { id: 139620, logo_path: null, name: 'Bioskopin21', origin_country: '' },
    ],
    production_countries: [
      { iso_3166_1: 'CN', name: 'China' },
      { iso_3166_1: 'US', name: 'United States of America' },
    ],
    release_date: '2020-09-04',
    revenue: 0,
    runtime: 115,
    spoken_languages: [{ iso_639_1: 'en', name: 'English' }],
    status: 'Released',
    tagline: '',
    title: 'Mulan',
    video: false,
    vote_average: 7.8,
    vote_count: 1042,
  };
  let dispatch = createEventDispatcher();
  const genres = details && details.genres && details.genres.map(genre => genre.name).join(' | ');

  onDestroy(() => {
    details = null;
  });
</script>

<article class="details">
  <nav aria-label="breadcrumb" class="breadcumb">
    <span on:click={() => dispatch('handleBackHome')}>Home</span>
    <span>{details.title}</span>
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
      <h1>{details.title}</h1>
      <p class="category">{genres}</p>
      <p class="rating">465456465</p>
      <p class="runtime">Length: {details.runtime}</p>
    </div>
  </header>
  <p class="overview">{details.overview}</p>

</article>
