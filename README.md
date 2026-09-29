# omarchy-media

Omarchy's media stack as a charly layer — the audio session client, players,
imaging and screen capture utilities its bindings and menus invoke.

The `omarchy-media` candy installs the client side of Omarchy's audio setup
(WirePlumber, ALSA utilities) plus the players (`mpv`, `mpv-mpris`,
`moonlight-qt`, `yt-dlp`, `omacut`, `kdenlive`, `obs-studio`), the imaging and
OCR tools (`imagemagick`, `libvips`, `ffmpegthumbnailer`, `pinta`, `tesseract`,
`tensaku`) and the screen recorder (`gpu-screen-recorder`). The PipeWire server
itself is **not** restated here: `pod-pipewire` owns it, and this candy requires
it rather than declaring a second copy.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `omarchy-media` |
| Requires | `layer-omarchy-base`, `pod-pipewire` (the audio server) |
| Players | `mpv`, `mpv-mpris`, `moonlight-qt`, `yt-dlp`, `omacut`, `kdenlive`, `obs-studio` |
| Imaging / OCR | `imagemagick`, `libvips`, `ffmpegthumbnailer`, `pinta`, `tesseract`, `tensaku`, `gtk4-layer-shell` |
| Capture | `gpu-screen-recorder` |
| Audio client | `wireplumber`, `alsa-utils` (the server is owned by `pod-pipewire`) |
| Service / port | none |

## How to use it

Compose the layer by pinning the member candy's sub-path in a desktop box's
`candy:` list:

```yaml
my-omarchy-desktop:
  candy:
    # the named box's value is the box BODY; `base:` and the `candy:` list are its keys
    base: omarchy
    candy:
      - '@github.com/opencharly/layer-omarchy-base/candy/omarchy-base:v2026.242.0701'
      - '@github.com/opencharly/layer-omarchy-media/candy/omarchy-media:v2026.242.0635'
```

## Layout

- `charly.yml` — repo shape: the `discover:` rule that finds the member candy.
- `candy/omarchy-media/charly.yml` — the candy entity (the `require:` deps, the
  `distro:` package arm, and the `plan:` `check:` assertions).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Closest family skill: `/charly-distros:omarchy-base` — the nearest owning procedure; this
  repo carries no `skill:` entity of its own.
- Audio server: `/charly-pod:pipewire`.
- Foundation: `/charly-distros:omarchy-base`.
- [`opencharly/opencharly](https://github.com/opencharly/opencharly) — the umbrella.
