# fledge-plugin-color

Color conversions and a browser color picker for [fledge](https://github.com/CorvidLabs/fledge).

Parse a color in HEX, RGB, or HSL; print HEX, RGB, HSL, and CMYK side-by-side with a true-color ANSI swatch right in your terminal. Or pop open a glassmorphic color picker in the browser.

## Install

```bash
fledge plugins install CorvidLabs/fledge-plugin-color
```

Requires `node` on PATH (the binary is a self-contained Node script — no `npm install` step).

## Usage

```bash
fledge color "#ff8800"                # parse hex
fledge color "rgb(0, 128, 255)"       # parse rgb()
fledge color "hsl(120, 100%, 50%)"    # parse hsl()
fledge color ui                       # open the web color picker
fledge color --help
```

### Terminal output

```text
fledge color "#ff8800"

      ← true-color ANSI swatch
      ←
Color Details:
  HEX:  #FF8800
  RGB:  rgb(255, 136, 0)
  HSL:  hsl(32, 100%, 50%)
  CMYK: cmyk(0%, 47%, 100%, 0%)
```

### Web UI

`fledge color ui` boots a small static server on `http://localhost:3000` and opens it in your default browser. The UI is a single-file `index.html` with no dependencies — a backdrop-blur glass card with live HEX/RGB/HSL/CMYK readouts. Ctrl+C to stop.

## How it works

This plugin runs via the [fledge-v1 plugin protocol](https://corvidlabs.github.io/fledge/). The `binary` field in `plugin.toml` points to `bin/color`, a single Node script that ships in the repo — no install step beyond `node` on PATH. The web UI is served from `ui/index.html` via Node's built-in `http` module.

## Development

```bash
# Run the CLI directly
chmod +x bin/color
./bin/color "#abc"
./bin/color ui

# Install locally for testing
fledge plugins install --path .
```

## License

MIT
