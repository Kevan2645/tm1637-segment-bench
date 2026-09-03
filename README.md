# Segment Bench

A browser-based simulator for a TM1637-style 4-digit 7-segment display. Design and preview text/number message sequences — with LONG / MEDIUM / SHORT display tiers and ~150ms refresh quantization matching typical embedded display-driver timing — without flashing any hardware.

Built for anyone developing firmware that drives a 4-digit 7-segment display and wants to iterate on message wording, sequencing, and timing before (or without) touching real hardware.

## Features

- **Live SVG display** — a faithful 7-segment rendering with real segment geometry (each segment has one fixed length, on real 7-segment hardware nothing resizes based on what else is lit).
- **Step sequence editor** — build a sequence of text and number steps, each with its own display duration (LONG / MEDIUM / SHORT, or a custom millisecond value).
- **Alphabet reference** — a built-in reference grid showing how every supported letter, digit, and symbol renders, flagged as either the common convention (matches most 7-segment alphanumeric fonts) or a more speculative approximation.
- **No auto-save** — edits are exploratory until you explicitly save. Nothing is silently persisted, so you can experiment freely without fear of clobbering a working sequence.
- **Save/load data files** — a plain `.json` file with just your tiers, brightness, and step list, named automatically from the sequence content — never a copy of the tool itself, so a fix made to this page benefits every sequence you've ever saved the next time you open it. Where your browser supports it (Chrome, Edge, and other Chromium browsers), saving and loading go through your OS's own native file dialogs, and every picker after the first remembers the folder you last used. Open several saved variants in separate tabs to compare them side by side.
- **Firmware target tagging** — an optional dropdown + note field that records which display state or cycle in your own firmware a sequence is meant to drive, saved and exported right alongside it.
- **JSON export** — export just the tier values, step list, and firmware target, ready to translate into your own firmware.

## Usage

Just open `segment-bench.html` in a browser — it's a single self-contained file, no build step, no server, no dependencies beyond a Google Font loaded from a CDN. Works from `file://` directly.

## Documentation

- [`guide.html`](guide.html) — full user guide: the display/transport controls, building a message, the alphabet's verified vs. approximate glyphs, saving/loading vs. exporting, and timing-tier quantization.
- [`quick-reference.txt`](quick-reference.txt) — a plain-text cheat sheet covering the same ground, for quick lookups.

## Customizing for your own display

The alphabet (`CHAR_MAP` near the top of the `<script>` block) is a straightforward character → segment-bitmask table. If your display's font differs from the common convention, or you want to add characters, just edit that table directly — no build tooling required.

The firmware target dropdown (`FIRMWARE_TARGETS`, also near the top of the `<script>` block) ships with two placeholder entries — edit that array to match the actual display-state names in your own firmware. The `id` of each entry is what gets written into a saved/exported file's `target` field, so once you've tagged sequences with an id, prefer changing its `label` over renaming the `id` itself; a saved file with a `target` that no longer matches anything in the list falls back to "Other" and folds the original value into the note rather than dropping it.

## License

MIT — see [LICENSE](LICENSE).
