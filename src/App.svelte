<script lang="ts">
  import { Movie } from "./services/Movies";
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";

  const movies = new Movie();
  let isLoading = true;
  let popular;
  let errorMessage = '';
  (async () => {
    try {
	  const popularResponse = await movies.popular({ page: 1 });
	  popular = popularResponse.data;
	  isLoading = false;
    } catch (error) {
		errorMessage = error;
		isLoading = false;
    }
  })();
</script>

<Header />
<main>
	<section>
		<h1>Popular Movies</h1>
		{#if isLoading}
			<p>Loading...</p>
		{/if}
		{#if errorMessage}
			<p>{ errorMessage }</p>
		{/if}
		{#if !isLoading && popular}
			<pre>{JSON.stringify(popular, null, 4)}</pre>
		{/if}
	</section>
</main>
<Footer />
