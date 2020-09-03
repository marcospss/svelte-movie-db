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
  import { Movie } from './services/Movies';
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';
  import Loading from './components/ui/Loading.svelte';
  import Tabs from './components/ui/Tabs.svelte';
  import PosterListCard from './components/PosterListCard.svelte';

  const movies = new Movie();
  let isLoading = true;
  let popular;
  let errorMessage = '';
  // https://swr.vercel.app/
  /**
   * POPULAR
   */
  const popularMovies = async () => {
    try {
      const popularResponse = await movies.popular({ page: 1 });
      popular = popularResponse.data;
      isLoading = false;
    } catch (error) {
      errorMessage = error;
      isLoading = false;
    }
  };

  // tabs
  let items = ['Popular Movies', 'Now Playing Movies', 'Upcoming Movies', 'Top Rated Movies'];
  let activeItem = 'Popular Movies';
  const tabChange = (e) => activeItem = e.detail;

  const handleAdd = () => {
    activeItem = 'Popular Movies';
  }

  onMount(async () => {
    await popularMovies();
  });
</script>

<Header />
<main>
    <Tabs {activeItem} {items} on:tabChange={tabChange} />
    {#if !isLoading && activeItem === 'Popular Movies'}
      <PosterListCard data={popular} />
    {/if}
    {#if isLoading}
      <Loading />
    {/if}
    {#if errorMessage}
      <p>{errorMessage}</p>
    {/if}
</main>
<Footer />
