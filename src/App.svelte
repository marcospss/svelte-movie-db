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

  onMount(async () => {
    await popularMovies();
  });
</script>

<Header />
<main>
    {#if isLoading}
      <Loading />
    {/if}
    {#if errorMessage}
      <p>{errorMessage}</p>
    {/if}
    {#if !isLoading && popular}
      <PosterListCard titleCollection="Popular Movies" data={popular} />
    {/if}
</main>
<Footer />
