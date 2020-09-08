<style>
  main {
    position: relative;
    padding-top: 4rem;
    min-height: calc(100vh - 184px);
    height: auto;
  }
</style>

<script lang="ts">
  import { onMount } from 'svelte';

  import MovieStore from './store/movieStore';
  import { Movie } from './services/Movies';
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';
  import Loading from './components/ui/Loading.svelte';
  import Tabs from './components/ui/Tabs.svelte';
  import PosterListCard from './components/PosterListCard.svelte';
  import Details from './components/Details.svelte';

  const movies = new Movie();
  $: isLoading = true;
  let data = null;
  $: detailsResponse = {};
  $: hasDetails = false;
  let errorMessage = '';

  // https://swr.vercel.app/
  /**
   * MOVIES
   */
  const dataMovies = async (service) => {
    try {
      isLoading = true;
      const response = await movies[service]({ page: 1 });
      data = response.data.results;
      MovieStore.update(() => [...data]);
      isLoading = false;
    } catch (error) {
      isLoading = false;
      errorMessage = error;
    }
  };

  /**
   * DETAILS
   */
  const handleLoadDetails = async (event) => {
    const {
      detail:mediaId,
    } = event;
    await dataDetails(mediaId);
  };

  const dataDetails = async (mediaId) => {
    try {
      isLoading = true;
      hasDetails = false;
      const response = await movies.details({mediaId});
      detailsResponse = await response.data;
      hasDetails = !!Object.keys(detailsResponse).length;
      isLoading = false;
    } catch (error) {
      isLoading = false;
      errorMessage = error;
    }
  };

  /**
   * PAGES
   */
  let pages = [
    {
      title: 'Now Playing Movies',
      slug: 'nowPlaying',
    },
    {
      title: 'Popular Movies',
      slug: 'popular',
    },
    {
      title: 'Top Rated Movies',
      slug: 'topRated',
    },
    {
      title: 'Upcoming Movies',
      slug: 'upcoming',
    },
  ];
  let activeItem = 'nowPlaying';
  const tabChange = async (event) => {
    const { slug } = event.detail;
    activeItem = slug;
    await dataMovies(slug);
  };

  /**
   * HANDLERS
   */
  const handleBackHome = () => hasDetails= false;

  onMount(async () => {
    await dataMovies(activeItem);
  });
</script>

<Header />
<main class="main-content">
  {#if !isLoading && !hasDetails && !errorMessage}
    <Tabs {activeItem} {pages} on:tabChange={tabChange} />
    <PosterListCard on:handleLoadDetails={handleLoadDetails} />
  {/if}
  {#if !isLoading && hasDetails }
    <Details {detailsResponse} on:handleBackHome={handleBackHome} />
  {/if}
  {#if isLoading}
    <Loading />
  {/if}
  {#if !isLoading && errorMessage}
    <p>{errorMessage}</p>
  {/if}
</main>
<Footer />
