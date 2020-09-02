<script lang="ts">
  import type { MovieItem } from '../../models/movie';
  export let content: MovieItem;
</script>

<style>
  .card {
    background: #fff;
    padding: 20px;
    border-radius: 6px;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  }
</style>

<div class="card">
  <h2>{ content }</h2>
</div>
