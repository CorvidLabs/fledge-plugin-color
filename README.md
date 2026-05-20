# fledge-plugin-color

A fledge plugin

## Install

```bash
fledge plugins install CorvidLabs/fledge-plugin-color
```

## Usage

```bash
fledge color
fledge color --help
```

## How it works

This plugin runs via the [fledge-v1 plugin protocol](https://corvidlabs.github.io/fledge/). The `binary` field in `plugin.toml` points to the executable in `bin/` — replace the starter bash stub with any language (Python, Node, Go, Rust, etc.). The only contract is that the binary is executable and supports `--help`.


## Development

```bash
# Test the command directly
chmod +x bin/*
./bin/color --help

# Install locally for testing
fledge plugins install --path .
```

## License

MIT
