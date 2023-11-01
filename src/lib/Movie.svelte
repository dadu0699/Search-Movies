<script lang="ts">
  export let title: string, poster: string, year: string;
</script>

<article class="card">
  <div class="content">
    <p class="title">
      {title}
      <span class="date">({year})</span>
    </p>
  </div>

  <img src={poster} alt={`Poster of the movie ${title}`} />
</article>

<style>
  .card {
    width: 200px;
    height: 250px;
    border-radius: 12px;
    overflow: hidden;
    position: relative;
    box-shadow:
      0 1px 3px rgba(0, 0, 0, 0.12),
      0 1px 2px rgba(0, 0, 0, 0.24);
    transition: all 300ms;
  }

  .card:hover {
    transform: translateY(-2px);
    box-shadow:
      0 14px 28px rgba(0, 0, 0, 0.25),
      0 10px 10px rgba(0, 0, 0, 0.22);
  }

  img {
    width: 100%;
    height: 100%;
    aspect-ratio: 16/9;
  }

  .content {
    box-sizing: border-box;
    width: 100%;
    position: absolute;
    padding: 30px 20px 20px 20px;
    height: auto;
    bottom: 0;
    background: linear-gradient(transparent, rgba(0, 0, 0, 1));
  }

  .date,
  .title {
    margin: 0;
  }

  .date {
    font-size: 12px;
    color: rgba(255, 255, 255, 0.9);
    margin-bottom: 4px;
  }

  .title {
    font-size: 17px;
    color: #fff;
  }
</style>
