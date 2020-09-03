<style>
  .tabs {
    display: flex;
    justify-content: flex-start;
    padding: 0;
    list-style-type: none;
    align-items: flex-end;
    margin: 2.5rem 0 0 0;
  }
  ul {
    display: flex;
    justify-content: center;
    padding: 0;
    margin: 0;
    list-style-type: none;
  }
  li {
    margin: 0 16px;
    font-size: 1.2rem;
    color: var(--color-primary);
    cursor: pointer;
  }
  .active {
    color: var(--color-secondary);
    border-bottom: 2px solid var(--color-secondary);
    padding-bottom: 8px;
  }
</style>

<script>
  import { createEventDispatcher } from 'svelte';
  let dispatch = createEventDispatcher();

  export let items;
  export let activeItem;
</script>

<div class="tabs">
  <ul>
    {#each items as item}
      <li on:click={() => dispatch('tabChange', item)}>
        <div class:active={item === activeItem}>{item}</div>
      </li>
    {/each}
  </ul>
</div>
