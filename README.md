# Jeormatter

Three compact custom formatters for [AIOStreams](https://docs.aiostreams.viren070.me/), with different ways to arrange the title, quality and filename.

Use **AIOStreams v2.35 or newer** for the visual-tag deduplication and forced-subtitle indicator.

## Choose a layout

| Formatter | Name field | Description |
| --- | --- | --- |
| [jeormatter.json](jeormatter.json) | Title, year and episode when available | Four lines: video, audio/subtitles, size, source |
| [jeormatter_alt.json](jeormatter_alt.json) | Resolution, quality, tier and visual tags | Four lines: title, audio/subtitles, size, source |
| [jeormatter_filename.json](jeormatter_filename.json) | Title, year and episode when available | Standard layout plus the original filename on a fifth line |

## Previews

These illustrative text previews use the same fictional movie and stream details for comparison. They are not screenshots; fonts, spacing and wrapping depend on your client. Conditional details appear only when the stream data and your configuration support them.

### Standard — jeormatter.json

Puts the movie or episode title in the name field, with technical details underneath.

**Name**

```text
Example Movie (2026)
```

**Description**

```text
✦ 4K · WEB-DL T1 · DV/HDR10
♬ DD+ 5.1 · EN · SUB EN · Forced
◈ 20 GiB · 25 Mbps
⛉ [RD] Torrentio · GROUP
```

[View formatter](jeormatter.json) · [Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter.json)

### Alternative — jeormatter_alt.json

Moves the video details into the name field, making resolution and quality easier to compare across results. The title becomes the first description line.

**Name**

```text
4K · WEB-DL T1 · DV/HDR10
```

**Description**

```text
✦ Example Movie (2026)
♬ DD+ 5.1 · EN · SUB EN · Forced
◈ 20 GiB · 25 Mbps
⛉ [RD] Torrentio · GROUP
```

[View formatter](jeormatter_alt.json) · [Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter_alt.json)

### Filename — jeormatter_filename.json

Uses the standard layout and adds the original filename at the bottom for checking release details.

**Name**

```text
Example Movie (2026)
```

**Description**

```text
✦ 4K · WEB-DL T1 · DV/HDR10
♬ DD+ 5.1 · EN · SUB EN · Forced
◈ 20 GiB · 25 Mbps
⛉ [RD] Torrentio · GROUP
Example.Movie.2026.2160p.WEB-DL.DDP5.1.DV.HDR10-GROUP.mkv
```

[View formatter](jeormatter_filename.json) · [Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter_filename.json)

## Reading the details

- **T1–T10** appears when a matching ranked stream expression supplies a tier, such as `Web T1`. It is not a rating the formatter calculates.
- **DV/HDR10** shows distinct visual tags. Duplicate entries are removed before display.
- **EN / SUB EN** reflects your configured audio and subtitle languages. Up to two codes are shown, with `+` when more match.
- **Forced** appears when a probed forced-subtitle track matches your configured subtitle languages. No badge does not prove forced subtitles are absent.
- **◈ / ❖** distinguishes an individual release from a season pack.
- **⛉ / ⛊** indicates an unproxied or proxied stream when that status is known.
- Other details can include library/preloading status, folder size, scores, SeaDex labels, network or edition, uncached status, P2P seeders and addon messages.

The examples assume a cached stream with no extra status messages. Missing data uses the formatter's fallbacks or is omitted.
