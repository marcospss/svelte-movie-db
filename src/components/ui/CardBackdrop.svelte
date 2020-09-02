<script lang="ts">
  import type { MovieItem } from '../../models/movie';
  import image from '../../settings/image';
  export let item: MovieItem;
  const processedOverview = (overview) => overview.length > 110 ? `${overview.substring(0, 100)}...` : overview;
</script>

<style>
  .card-backdrop-item {
    background: var(--color-white);
    border-radius: .5rem;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    overflow: hidden;
  }
  .card-backdrop-item .header {
    position: relative;
  }
  .card-backdrop-item .header figure {
    padding: 0;
    margin: 0;
  }
  .card-backdrop-item .header img {
    width: 100%;
    margin: 0;
    padding: 0;
  }
  .card-backdrop-item .header h1 {
    width: 100%;
    position: absolute;
    bottom: 4px;
    left: 0;
    margin: 0;
    background-color: #fff6;
    padding: 0.5rem;
    font-size: 1.5rem;
    color: var(--color-secondary);
    font-weight: normal;
    box-shadow: 0px 0px 4px 2px rgba(158,158,158,0.5);
    overflow: hidden;
  }
  .card-backdrop-item .overview {
    padding: 10px 20px;
    line-height: 1.2rem;
  }
</style>

<article class="card-backdrop-item">
  <div class="header">
    <figure>
      <img src={`${image.secure_base_url}${image.backdrop_sizes.w300}${item.backdrop_path}`}  alt={item.title} />
    </figure>
    <h1>{ item.title }</h1>
  </div>
  <p class="overview">{ processedOverview(item.overview) }</p>
</article>
