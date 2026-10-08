# Jeormatter

A clean, compact formatter for AIOStreams. See the title, video quality, audio, languages and source at a glance.

Requires **AIOStreams v2.35 or newer**.

## Pick your layout

All three show the same details. Choose where you want the title, or add the filename.

### Standard

Title first, details underneath.

[Download standard JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter.json)

```text
Example Movie (2026)
✓ 4K · Remux T1 · DV/HDR10
♬ Atmos · TrueHD (7.1)
≡  EN (+Comm) · SUB EN (+SDH)
◈ 20 GiB · 25 Mbps
⛉  [TB] Torrentio · GROUP
```

### Video first

Swaps the title and video-quality row. Everything else stays the same.

[Download video-first JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter_alt.json)

```text
✓ 4K · Remux T1 · DV/HDR10
Example Movie (2026)
♬ Atmos · TrueHD (7.1)
≡  EN (+Comm) · SUB EN (+SDH)
◈ 20 GiB · 25 Mbps
⛉  [TB] Torrentio · GROUP
```

### With filename

The standard layout, with the full filename at the bottom.

[Download filename JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter_filename.json)

```text
Example Movie (2026)
✓ 4K · Remux T1 · DV/HDR10
♬ Atmos · TrueHD (7.1)
≡  EN (+Comm) · SUB EN (+SDH)
◈ 20 GiB · 25 Mbps
⛉  [TB] Torrentio · GROUP
Example.Movie.2026.2160p.TrueHD.7.1-GROUP.mkv
```

## How to use

1. Download the JSON for your preferred layout.
2. Import it into AIOStreams' custom formatter settings.
3. Preview it, then save your configuration.

To update, import the file again. An already-imported copy won't pick up changes from this repository automatically.

## Reading the details

| Symbol | Meaning |
| --- | --- |
| ✓ | In your library |
| ➤ | Preloading |
| ✦ | Video details |
| ♬ | Audio details |
| ≡ | Audio and subtitle languages |
| ◈ / ❖ | Single release / season pack |
| ⛉ / ⛊ | Direct / proxied stream |
| ⏳ | Uncached |
| ★ | SeaDex Best |

- **EN, JA, etc.** are language codes. **SUB** introduces subtitle languages.
- **Comm** means commentary; **AD** means audio description.
- **Forced**, **SDH**, **Signs** and **Dub** identify forced subtitles, accessibility subtitles, signs, and dubtitles.
- **EN (+Comm)** means regular English and a commentary track are available. **EN (Comm)** means only a commentary-labelled English track was reported.
- **T1, T2, etc.** come from your AIOStreams ranking rules.
- **Director's Cut**, **Extended** and similar editions appear beside the title when known.

For season packs, the first size is the file and the second is the whole pack:

```text
❖ 6.95 GiB / 211 GiB · 6.75 Mbps
```

Short language details stay on the audio row. Longer ones get their own row. Missing details are left out; a missing subtitle row doesn't necessarily mean there are no subtitles.

These are sample previews. Spacing and wrapping depend on your player, which may also add its own size line.

## Credits

Built for [AIOStreams](https://docs.aiostreams.viren070.me/), with ideas from [Tamtaro's formatters and sorting setup](https://github.com/Tam-Taro/SEL-Filtering-and-Sorting).
