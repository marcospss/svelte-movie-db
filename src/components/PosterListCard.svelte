<style>
  .poster-list {
    padding: 0 42px 42px;
    width: 100%;
  }
  .poster-list .grid-list {
    display: grid;
    width: 100%;
    grid-template-columns: 1fr;
    row-gap: 1rem;
  }

  @media screen and (min-width: 600px) and (max-width: 801px) {
    .poster-list .grid-list {
      grid-template-columns: repeat(2, 1fr);
      column-gap: 1rem;
    }
  }

  @media screen and (min-width: 801px) {
    .poster-list .grid-list {
      grid-template-columns: repeat(3, 1fr);
      column-gap: 1rem;
    }
  }
</style>

<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  import MovieStore from '../store/movieStore';
  import CardPoster from './ui/CardPoster.svelte';

  export let title;
</script>

<section class="poster-list">
  <h2>{title}</h2>
  <div class="grid-list">
    {#each $MovieStore as item (item.id)}
      <CardPoster {item} />
    {/each}
  </div>
</section>
