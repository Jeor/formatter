# Jeormatter

Custom formatters for [AIOStreams](https://docs.aiostreams.viren070.me/). Use **AIOStreams v2.35 or newer** for track-aware formatting.

## Choose a layout

| Formatter | Layout |
| --- | --- |
| [jeormatter.json](jeormatter.json) | Current title-first formatter: compact category rows, regular text, grouped track labels and independent editions |
| [jeormatter_alt.json](jeormatter_alt.json) | Earlier quality-first version; retains its original slash-separated tracks, codec and score display |
| [jeormatter_filename.json](jeormatter_filename.json) | Earlier title-first version with the full filename; retains its original formatting |

The refinements below apply to **jeormatter.json**. The alternative and filename files remain unchanged.

## Current formatter

[Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter.json)

Example output with probed English audio, an additional commentary track, and regular plus SDH subtitles:

```text
Example Movie (2026)
➤ 4K · Remux T1 · DV/HDR10
♬ Atmos · TrueHD (7.1)
≡ EN (+Comm) · SUB EN (+SDH)
◈ 20 GiB · 25 Mbps
⛉ [TB] Torrentio · GROUP
```

The title is the name field; the remaining rows are the description. These text examples use fictional stream data. Client fonts and wrapping vary. Your player may append its own size footer.

Short language information stays on the audio row. Missing language/subtitle information adds no empty row:

```text
Example Episode · S01 · E01
✦ 1080p · Bluray
♬ FLAC (5.1) · JA
❖ 6.95 GiB / 211 GiB · 6.75 Mbps
⛉ [TB] Torrentio · GROUP
```

Edition/cut information appears beside the title independently of source/network information. Upscaled is displayed only when the corresponding RSE matches:

```text
Example Movie (2026) · Director's Cut
✦ 4K · Remux T1 · DV/HDR10 · Upscaled
♬ Atmos · TrueHD · (7.1, 5.1)
◈ 20 GiB · 25 Mbps
⛉ [TB] Torrentio · GROUP · MA
```

Here the channel list is separated by a dot because probed format/channel pairing is unavailable.

## Reading the current formatter

- **Video:** resolution, quality, matching RSE tier, and distinct visual tags. Video codec (`stream.encode`) is omitted. Audio format, channel and visual-tag text is not truncated.
- **Audio:** dot-separated formats. With suitable probed tracks, each format receives its highest reported channel layout among your configured languages, excluding commentary/audio-description tracks using flags and title hints. This describes available tracks, not the player's selection. Atmos remains a stream-level tag. Without suitable track data, formats and channel layouts are shown as separate groups rather than pretending they are paired.
- **Languages:** tracks are filtered using your configured audio/subtitle languages. Repeated languages are grouped. Multiple languages use commas.
- **Track labels:** `Comm`, `AD`, `Forced`, `SDH`, `Signs`, and `Dub` (explicit dubtitle) use track flags and title hints. Signs are not automatically forced; CC is not automatically a dubtitle.
- **Additional variants:** `EN (+Comm)` means an unflagged English track also exists; `EN (Comm)` means only commentary-labelled English tracks were reported. Subtitle variants use the same convention. An unflagged track is not proof of completeness or correctness.
- **Unknown subtitles:** omit missing information; never display “no subtitles.” Filename-derived language information can be incomplete or ambiguous. A release marked subbed without language details can display `SUB`.
- **Adaptive rows:** conservative format-length and track-count checks move longer language details to a `≡` row. JSON cannot measure the client's pixel width; natural wrapping still depends on the player.
- **Size:** `◈` for a single release and `❖` for a season pack. A positive folder size is appended for season packs; bitrate appears when known.
- **Leading status:** the video row uses `☁︎` for library, otherwise `➤` for preloading, otherwise `✦`. The source row gives `⏳` uncached status priority, then `⛊` proxy, `★` SeaDex Best, or `⛉` unproxied status when known. Cached streams have no cache badge. Category/status symbols are kept at row starts.
- **Source:** service abbreviation, usenet indexer or addon, release group, SeaDex Best/Alt and network information. P2P seeders and addon status messages remain available when applicable. Numeric sorting scores are omitted. Source/group names retain their compact length limits.

## RSE and edition behavior

The quality tier comes from explicit RSE names: Remux T1–T10; UHD/HD BluRay, BD or BluRay T1–T10; and Web T1–T10. It is not a rating calculated by the formatter. iTunes and Movies Anywhere RSE matches can provide source labels.

The edition display combines selected RSE matches and parsed edition fields. Supported aliases include Director's Cut, Extended, Theatrical, Open Matte, IMAX/IMAX Enhanced, Remaster/4K Remaster, Color Corrected, Hybrid and Uncensored. Case and supported straight/curly-apostrophe aliases are deduplicated. More specific IMAX Enhanced and 4K Remaster labels suppress their generic counterparts. Other parsed editions are retained and deduplicated case-insensitively.

The `Upscaled` RSE label is displayed when matched. It is a rule-derived hint, not a technical inspection. **Generated DV/HDR10+ is deliberately not displayed.** Other ranking matches, boosts and scores are not dumped into the card.

RSE/track ideas draw on [Tamtaro's setup](https://github.com/Tam-Taro/SEL-Filtering-and-Sorting/blob/main/AIOStreams%20Templates/Tamtaro-complete-setup-template.json) and its linked rules. Enabled rules depend on your template choices.

## Earlier layouts

### Alternative — jeormatter_alt.json

```text
4K · WEB-DL T1 · HEVC · DV/HDR10
✦ Example Movie (2026)
♬ DD+ 5.1
  EN/EN[AD] · SUB EN/EN[F]+
◈ 20 GiB · 25 Mbps
⛉ [RD] Torrentio · GROUP
```

[Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter_alt.json)

### Filename — jeormatter_filename.json

```text
Example Movie (2026)
✦ 4K · WEB-DL T1 · HEVC · DV/HDR10
♬ DD+ 5.1
  EN/EN[AD] · SUB EN/EN[F]+
◈ 20 GiB · 25 Mbps
⛉ [RD] Torrentio · GROUP
Example.Movie.2026.2160p.WEB-DL.HEVC.DDP5.1.DV.HDR10-GROUP.mkv
```

[Raw JSON](https://raw.githubusercontent.com/Jeor/formatter/main/jeormatter_filename.json)

## Validation

The current JSON was parsed and rendered locally with the upstream AIOStreams formatter engine against fixtures covering grouped tracks, channel pairing, missing data, edition aliases, season packs, and cache status. It has not yet been verified in an Apple playback client. Test the imported formatter using AIOStreams' Preview before relying on client-specific wrapping.
