<style>
  section {
    padding: 14px;
  }
  section .grid-list {
    display: grid;
    grid-template-columns: 1fr;
    row-gap: 1rem;
  }

  @media screen and (min-width: 600px) and (max-width: 801px) {
    section .grid-list {
      grid-template-columns: repeat(2, 1fr);
      column-gap: 1rem;
    }
  }

  @media screen and (min-width: 801px) and (max-width: 1024px) {
    section .grid-list {
      grid-template-columns: repeat(3, 1fr);
      column-gap: 1rem;
    }
  }

  @media (min-width: 1024px) {
    section .grid-list {
      grid-template-columns: repeat(4, 1fr);
      column-gap: 1rem;
    }
  }
</style>

<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { fade, slide, scale } from 'svelte/transition';
  import { flip } from 'svelte/animate';
  
  import MovieStore from '../store/movieStore';
  import CardBackdrop from './ui/CardBackdrop.svelte';

  let dispatch = createEventDispatcher();

</script>

<section>
  <div class="grid-list">
    {#each $MovieStore as item (item.id)}
    <div in:fade out:scale|local animate:flip={{duration: 500}} on:click={() => dispatch('handleLoadDetails', item.id)}>
      <CardBackdrop {item} />
    </div>
    {/each}
  </div>
</section>
