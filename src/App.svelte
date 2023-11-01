<script lang="ts">
  import Input from '@/lib/Input.svelte';
</script>

<main class="container">
  <h1>Search Movies 🍿</h1>
  <Input />
</main>

<style>
  .container {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
    margin-left: auto;
    margin-right: auto;
    padding: 1.5rem;
    width: 100%;
  }

  .container h1 {
    align-self: center;
    font-weight: 900;
    text-align: center;
  }

  @media (min-width: 640px) {
    .container {
      max-width: 640px;
    }
  }

  @media (min-width: 768px) {
    .container {
      max-width: 768px;
    }
  }

  @media (min-width: 1024px) {
    .container {
      max-width: 1024px;
    }
  }
</style>
