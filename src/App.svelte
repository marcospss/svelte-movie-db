<script lang="ts">
  import { onMount } from 'svelte';
  import { Movie } from './services/Movies';
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';

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
  <section>
    <h1>Popular Movies</h1>
    {#if isLoading}
      <p>Loading...</p>
    {/if}
    {#if errorMessage}
      <p>{errorMessage}</p>
    {/if}
    {#if !isLoading && popular}
      <pre>{JSON.stringify(popular, null, 4)}</pre>
    {/if}
  </section>
</main>
<Footer />
