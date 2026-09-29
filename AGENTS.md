# AGENTS.md — layer-omarchy-media

Standalone candy repo for the Omarchy media layer — the audio session client,
players, imaging and screen-capture utilities its bindings and menus invoke. The
repo is multi-candy-shaped: the root `charly.yml` carries only the repo shape
(`discover:`), and the member candy lives in `candy/omarchy-media/charly.yml`.

This repo has **no `skill:` entity** in its candy manifest, so there is no
dedicated owning skill projected into the marketplace corpus. The gap is recorded
against `opencharly/opencharly#291` (the batch that authors missing `skill:`
entities).

Canonical files:

- `charly.yml` — the repo shape (`repo:` + `discover:`).
- `candy/omarchy-media/charly.yml` — the candy entity: the `require:` deps, the
  `distro:` package arm, and the `plan:` `check:` assertions.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-distros:omarchy-base` — the family foundation skill: the package
  sources, the pinned mirror snapshot, and the runtime this layer builds on.
  Load before editing or troubleshooting.
- `/charly-pod:pipewire` — the audio server this candy requires but does not own.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, and service declarations). Load before editing any entity field or
  plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence — they assert
  the players, the imaging/OCR tools, the audio client, and the screen recorder.

## Modify this repo

- There is no `skill:` entity to keep in sync; if one is added (per #291), it
  must be edited together with the candy entity in the same change.
- Keep the audio **server** out: `pod-pipewire` owns it; this candy installs
  clients only. One owner per behaviour (R3).
- Assert the screen recorder via `command -v`, not a fixed `/usr/bin` path — the
  package installs it to `/usr/sbin`, which is a symlink to `/usr/bin` on Arch.
- New behaviour claims belong in the `plan:` as an observable `check:` step.

## Landing

- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo — read it
  before landing.
- Release history lives in `CHANGELOG/`.
