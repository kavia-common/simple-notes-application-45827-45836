<script lang="ts">
  import "../app.css";
  import Header from "$lib/components/Header.svelte";
  let { children } = $props();
</script>

<div class="app">
  <Header title="Simple Notes" />
  <main class="content">
    {@render children()}
  </main>
</div>

<style>
  .app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    background: var(--ocean-bg);
  }
  .content {
    display: flex;
    flex: 1;
    max-width: 1200px;
    margin: 16px auto;
    width: 100%;
    gap: 16px;
    padding: 0 16px 16px;
  }
  @media (max-width: 900px) {
    .content {
      flex-direction: column;
      margin: 8px auto;
    }
  }
</style>
