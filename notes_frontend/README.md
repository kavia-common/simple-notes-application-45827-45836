# Simple Notes Frontend (Svelte)

A single-page notes app with a two-pane layout (sidebar + editor) implementing create, view, edit, and delete with localStorage persistence. Styled with the "Ocean Professional" theme: primary #2563EB and secondary #F59E0B with subtle shadows, rounded corners, and smooth transitions.

- Port: 3000
- Tech: SvelteKit
- Persistence: localStorage (no backend required)
- Optional env: VITE_API_BASE or VITE_BACKEND_URL (reserved for future API provider)

## Develop

Install and run:

```bash
npm install
npm run dev
```

Then open http://localhost:3000.

## Build

```bash
npm run build
npm run preview
```

## Environment

If you later add a backend, expose one of:
- `VITE_API_BASE` or
- `VITE_BACKEND_URL`

The UI will still default to localStorage unless a provider swap is implemented; the code is structured to make this straightforward.
