# Jeormatter

Three compact custom formatters for [AIOStreams](https://docs.aiostreams.viren070.me/), with different ways to arrange the title, quality and filename.

Use **AIOStreams v2.35 or newer** for the visual-tag deduplication and per-language track labels.

## Choose a layout

| Formatter | Name field | Description |
| --- | --- | --- |
| [jeormatter.json](jeormatter.json) | Title, year and episode when available | Four lines: video, audio/subtitles, size, source |
| [jeormatter_alt.json](jeormatter_alt.json) | Resolution, quality, tier, codec and visual tags | Four lines: title, audio/subtitles, size, source |
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
✦ 4K · WEB-DL T1 · HEVC · DV/HDR10
♬ DD+ 5.1 · EN/EN[AD] · SUB EN/EN[Forced]/EN[SDH]
◈ 20 GiB · 25 Mbps
⛉ [RD] Torrentio · GROUP
```

[View formatter](jeormatter.json) · [Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter.json)

### Alternative — jeormatter_alt.json

Moves the video details into the name field, making resolution and quality easier to compare across results. The title becomes the first description line.

**Name**

```text
4K · WEB-DL T1 · HEVC · DV/HDR10
```

**Description**

```text
✦ Example Movie (2026)
♬ DD+ 5.1 · EN/EN[AD] · SUB EN/EN[Forced]/EN[SDH]
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
✦ 4K · WEB-DL T1 · HEVC · DV/HDR10
♬ DD+ 5.1 · EN/EN[AD] · SUB EN/EN[Forced]/EN[SDH]
◈ 20 GiB · 25 Mbps
⛉ [RD] Torrentio · GROUP
Example.Movie.2026.2160p.WEB-DL.HEVC.DDP5.1.DV.HDR10-GROUP.mkv
```

[View formatter](jeormatter_filename.json) · [Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter_filename.json)

## Reading the details

- **T1–T10** appears when a matching ranked stream expression supplies a tier, such as `Web T1`. It is not a rating the formatter calculates.
- **DV/HDR10** shows distinct visual tags. Duplicate entries are removed before display.
- **HEVC / AVC / AV1** shows the video codec when known.
- **EN / SUB EN** reflects your configured audio and subtitle languages. When matching probed tracks exist, each language carries its own labels. Up to three distinct rendered entries are shown per audio/subtitle list, with `+` when more exist. Duplicate entries are removed. Otherwise, the original fallback shows up to two language codes with `+` for more.
- **[AD] / [Comm]** identifies audio description or commentary using track flags and descriptive track titles.
- **[Forced]** checks the forced flag or a track title containing `forced`.
- **[SDH]** checks the hearing-impaired flag, a title containing `SDH` or `closed caption`, or a title equal to `CC`. It also applies to anime; CC alone is not treated as a dubtitle.
- **[Signs] / [Dub]** identifies track titles containing `signs` or `dubtitle`. Signs are not automatically marked as forced. A track can carry multiple labels.
- Track-title checks are case-insensitive hints, not guarantees. Missing labels do not prove those track types are absent. Track labels describe available tracks, not the player's current selection.
- **◈ / ❖** distinguishes an individual release from a season pack.
- **⛉ / ⛊** indicates an unproxied or proxied stream when that status is known.
- Other details can include library/preloading status, folder size, scores, SeaDex labels, network or edition, uncached status, P2P seeders and addon messages.

The examples assume a cached stream with no extra status messages. Missing data uses the formatter's fallbacks or is omitted.

## Track-label examples

Depending on the available metadata, the language portion can show:

```text
EN/EN[Comm]                  Audio with a commentary track
EN[AD]                       Audio description
SUB EN[Forced]               Forced subtitle track
SUB EN[SDH]                  Subtitles for deaf/hard-of-hearing viewers
SUB EN[Signs]/EN[Dub]         Separate signs and explicitly named dubtitles
SUB EN/EN[Forced]/EN[SDH]+    More than three distinct subtitle entries
```

Track-detail ideas were inspired by [Tam-Taro's v3.2.9 formatters](https://github.com/Tam-Taro/SEL-Filtering-and-Sorting/blob/main/CHANGELOG.md#329-2026-10-05), adapted to Jeormatter's compact layouts and conservative labels.
