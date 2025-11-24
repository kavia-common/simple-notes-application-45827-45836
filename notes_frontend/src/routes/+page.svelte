<script lang="ts">
  import NotesList from "$lib/components/NotesList.svelte";
  import NoteEditor from "$lib/components/NoteEditor.svelte";
  import { notesStore } from "$lib/stores/notes";

  // local reactive state using Svelte runes
  let state = $state<{ notes: ReturnType<typeof notesStore.getAll>; selectedId: string | null }>({
    notes: [],
    selectedId: null
  });

  // subscribe to store to refresh local state for template
  $effect(() => {
    const unsub = notesStore.subscribe((s) => {
      state.notes = s.notes;
      state.selectedId = s.selectedId;
    });
    return () => unsub();
  });

  // Initialize with a welcome note if empty (run after first subscription tick)
  $effect.pre(() => {
    if (state.notes.length === 0) {
      const welcome = notesStore.create("Welcome 👋", "Start typing your first note here.");
      notesStore.select(welcome.id);
    }
  });

  function selectedNote() {
    return state.notes.find((n) => n.id === state.selectedId) ?? null;
  }
</script>

<svelte:head>
  <title>Simple Notes</title>
  <meta name="description" content="A simple notes app built with Svelte. Ocean Professional theme." />
</svelte:head>

<div class="pane">
  <div class="sidebar-wrap card">
    <NotesList notes={state.notes} selectedId={state.selectedId} />
  </div>
  <div class="editor-wrap card">
    <NoteEditor note={selectedNote()} />
  </div>
</div>

<style>
  .pane {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 16px;
    width: 100%;
    min-height: calc(100vh - 120px);
  }
  .card {
    background: var(--ocean-surface);
    border: 1px solid var(--ocean-border);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    overflow: hidden;
  }
  .sidebar-wrap {
    min-height: 480px;
  }
  .editor-wrap {
    min-height: 480px;
    display: flex;
  }

  @media (max-width: 900px) {
    .pane {
      grid-template-columns: 1fr;
      min-height: auto;
    }
    .sidebar-wrap, .editor-wrap {
      min-height: 360px;
    }
  }
</style>
