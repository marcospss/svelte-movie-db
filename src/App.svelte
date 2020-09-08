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

  const movies = new Movie();
  $: isLoading = true;
  let data = null;
  let errorMessage = '';
  
  // https://swr.vercel.app/
  /**
   * POPULAR
   */
  const dataMovies = async (service = 'nowPlaying') => {
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

  // tabs
  let pages = [
    {
    title: 'Now Playing Movies',
    slug: 'nowPlaying'
    },
    {
    title: 'Popular Movies',
    slug: 'popular'
    },
    {
    title: 'Top Rated Movies',
    slug: 'topRated'
    },
    {
    title: 'Upcoming Movies',
    slug: 'upcoming'
    },
  ];
  let activeItem = 'nowPlaying';
  const tabChange = async (e) => {
    const { slug } = e.detail;
    activeItem = slug;
    await dataMovies(slug);
  };

  onMount(async () => {
    await dataMovies();
  });
</script>

<Header />
<main class="main-content">
    <Tabs {activeItem} {pages} on:tabChange={tabChange} />
    {#if !isLoading && !errorMessage}
      <PosterListCard />
    {/if}
    {#if isLoading}
      <Loading />
    {/if}
    {#if !isLoading && errorMessage}
      <p>{errorMessage}</p>
    {/if}
</main>
<Footer />
