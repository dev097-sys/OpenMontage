# AI Art Film Factory

A tablet-friendly, local-first planning dashboard that lives alongside OpenMontage. It is deliberately separate from `backlot/`, the production pipeline, and Remotion.

## Open it

Open `film-factory/index.html` in a browser, or enable GitHub Pages for this repository and publish from the feature branch with the folder set to `/film-factory`. The app is static: no build step, backend, account, or API key is required.

## What it does

- Create multiple 10-, 30-, and 90-minute film projects (runtime is editable).
- Store a film brief, synopsis, visual style bible, sound direction, continuity notes, and references.
- Create and edit a scene/shot list; track each scene through planned, prompt-ready, generating, review, approved, or failed.
- Track basic production progress.
- Export/import portable JSON project manifests for backups and handoff to an OpenMontage agent or a Colab notebook.
- Work on mobile/tablet screens and save project data in browser localStorage.

## Handoff contract

The export uses schema identifier `openmontage.film-factory.project.v1`. It contains the project brief and scenes, plus a note that it is a planning handoff. It is not yet an executable OpenMontage pipeline manifest. Before running a production, map the approved brief and scene plan into the repository's canonical artifacts and pipeline stages:

`idea -> script -> scene_plan -> assets -> edit -> compose -> publish`

Keep OpenMontage's existing project artifacts, approval gates, provider selection, and Backlot as the source of truth for actual production state.

## Important limits

- This dashboard does not generate images/video, launch Colab jobs, or call OpenMontage's Python tools.
- It does not include provider API credentials. Do not add API keys to browser storage or exported JSON; use Colab Secrets or local environment variables.
- Colab free GPU access and session limits are variable; a 10–90 minute film must be assembled from many shorter shots and may require substantial generation time, storage, and/or paid provider usage.
- Data is stored only in the current browser profile on the current device. Export JSON backups before clearing browser data or switching devices.
- Reference links are stored as text. Uploaded reference images and generated media are not embedded in the manifest.

## Safe extension point

The dashboard is an independent static companion. Integrate it with the pipeline only after defining and validating a versioned adapter between its export schema and OpenMontage's canonical artifacts. Do not write directly into active project directories or bypass creative approval gates.
