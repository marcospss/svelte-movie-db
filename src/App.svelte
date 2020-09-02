<script lang="ts">
  import { onMount } from 'svelte';
  import { Movie } from './services/Movies';
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';

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

  onMount(() => {
    popularMovies();
  });
</script>

<Header />
<main>
    {#if isLoading}
      <p>Loading...</p>
    {/if}
    {#if errorMessage}
      <p>{errorMessage}</p>
    {/if}
    {#if !isLoading && popular}
      <PosterListCard titleCollection="Popular Movies" data={popular} />
    {/if}
</main>
<Footer />
