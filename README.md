# MLT Encoding Tileserver Debug Cases

Test cases for isolating the effect of the `encoding: mlt` parameter in different positions.

## Setup

Start a local HTTP server from the workspace root:

```bash
./bin/start-server
```

This runs `python3 -m http.server 8000` with the workspace as the document root, so
source TileJSON is reachable at `http://localhost:8000/sources/<filename>`.

Open `http://localhost:8000` in a browser to view the map with a style switcher.

## Sources

| File | `encoding: mlt` in TileJSON |
|---|---|
| `sources/no_encoding.json` | No |
| `sources/mlt_encoding.json` | Yes |

Both sources serve tiles from:
```
https://demotiles.maplibre.org/tiles-mlt/plain/{z}/{x}/{y}.mlt
```

## Styles

Each style varies two independent axes:

1. **TileJSON encoding** — does the TileJSON returned by the source URL include `"encoding": "mlt"`?
2. **Style source encoding** — does the `sources.maplibre` object inside the style itself include `"encoding": "mlt"`?

| Style file | TileJSON `encoding: mlt` | Style source `encoding: mlt` |
|---|---|---|
| `styles/no_style_encoding_no_tile_encoding.json` | No | No |
| `styles/no_style_encoding_mlt_tile_encoding.json` | No | Yes |
| `styles/mlt_style_encoding_no_tile_encoding.json` | Yes | No |
| `styles/mlt_style_encoding_mlt_tile_encoding.json` | Yes | Yes |
