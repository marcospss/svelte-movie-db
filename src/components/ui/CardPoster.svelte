<style>
  .card-poster-item {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    background-color: var(--color-white);
    box-shadow: 0 5px 10px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    margin-bottom: 1rem;
    border-radius: 0.5rem;
    width: 100%;
    max-height: 150px;
    overflow: hidden;
  }

  .poster {
    position: relative;
    margin: 0;
    width: 141px;
    overflow: hidden;
    cursor: pointer;
  }

  .poster img {
    height: 100%;
  }

  .content {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    width: 100%;
    padding: 1rem;
  }

  .content .title {
    font-size: 1rem;
    margin: 0 0 0.5rem;
  }

  .content .overview {
    position: relative;
    margin: 0 0 0.5rem;
    height: 50px;
    overflow: hidden;
    line-height: 1rem;
    font-size: 0.9rem;
  }

  .content .overview::after {
    content: '';
    text-align: right;
    bottom: -10px;
    left: 0px;
    width: 100%;
    height: 60px;
    background: linear-gradient(180deg, rgba(255, 255, 255, 0.1), var(--color-white));
    display: flex;
    position: absolute;
    overflow: hidden;
  }

  .content .btn-learn-more {
    align-self: flex-end;
    font-size: 0.75rem;
    padding: 0.5rem 0.75rem;
    color: var(--color-white);
    border: none;
    border-radius: 0.25rem;
    background-color: #2d3748;
    font-weight: 500;
    cursor: pointer;
  }
</style>

<script lang="ts">
  import type { MovieItem } from '../../models/movie';
  import image from '../../settings/image';
  export let item: MovieItem;

  const Processedtitle = item.title.length > 28 ? `${item.title.substring(0, 28)}...` : item.title;
</script>

<div class="card-poster-item">
  <figure class="poster">
    <img
      src={`${image.secure_base_url}${image.poster_sizes.w92}${item.poster_path}`}
      alt={item.title}
    />
  </figure>
  <div class="content">
    <h2 class="title">{item.title}</h2>
    <p class="overview">{item.overview}</p>
    <!-- <button
      type="button"
      class="btn-learn-more"
      on:click={handleLoadDetails(item.id)}
    >Learn More</button> -->
  </div>
</div>
