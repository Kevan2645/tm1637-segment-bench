# Segment Bench

A browser-based simulator for a TM1637-style 4-digit 7-segment display. Design and preview text/number message sequences — with LONG / MEDIUM / SHORT display tiers and ~150ms refresh quantization matching typical embedded display-driver timing — without flashing any hardware.

Built for anyone developing firmware that drives a 4-digit 7-segment display and wants to iterate on message wording, sequencing, and timing before (or without) touching real hardware.

## Features

- **Live SVG display** — a faithful 7-segment rendering with real segment geometry (each segment has one fixed length, on real 7-segment hardware nothing resizes based on what else is lit).
- **Step sequence editor** — build a sequence of text and number steps, each with its own display duration (LONG / MEDIUM / SHORT, or a custom millisecond value).
- **Alphabet reference** — a built-in reference grid showing how every supported letter, digit, and symbol renders, flagged as either the common convention (matches most 7-segment alphanumeric fonts) or a more speculative approximation.
- **No auto-save** — edits are exploratory until you explicitly save. Nothing is silently persisted, so you can experiment freely without fear of clobbering a working sequence.
- **Save as file** — export a complete, standalone copy of the tool with your sequence embedded, named automatically from the sequence content. Open several saved variants in separate tabs to compare them side by side.
- **JSON export** — export just the tier values and step list, ready to translate into your own firmware.

## Usage

Just open `segment-bench.html` in a browser — it's a single self-contained file, no build step, no server, no dependencies beyond a Google Font loaded from a CDN. Works from `file://` directly.

## Customizing for your own display

The alphabet (`CHAR_MAP` near the top of the `<script>` block) is a straightforward character → segment-bitmask table. If your display's font differs from the common convention, or you want to add characters, just edit that table directly — no build tooling required.

## License

MIT — see [LICENSE](LICENSE).
