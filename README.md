# Delfin

Stream movies and TV shows from Jellyfin.

Originally forked from https://codeberg.org/avery42/delfin.

## Features/Roadmap

The following features are currently implemented or planned:

- Direct playback
- Movie collections
- TV show collections
- [Jellyscrub](https://github.com/nicknsy/jellyscrub/) (scrubber thumbnails) plugin support
- [Intro Skipper](https://github.com/ConfusedPolarBear/intro-skipper/) plugin support
- *Music collections (planned)*
- *Live TV (planned)*
- *Library search (planned)*
- *Syncplay (planned)*
- *Transcoded playback (planned)*

These features will be added as part of this fork and (hopefully) revival of this project, with more coming too:

- Managing your collections
- Server administration
- Book collections

## Development Setup

### Easiest: Docker (no host deps)
1. Build the dev image: `sudo docker build -f Dockerfile.dev -t delfin-dev .`
2. Run a shell:  
   `sudo docker run --rm -it -v "$PWD":/workspace -v delfin-cargo-cache:/usr/local/cargo/registry -v delfin-target:/workspace/target delfin-dev bash`
3. Inside the container: `cargo build` (and `cargo test`, `cargo audit`).
4. To produce a host-usable binary in `./target/release` without an interactive shell:  
   ```bash
   sudo docker run --rm \
     -v "$PWD":/workspace \
     -v "$PWD/target":/workspace/target \
     -v delfin-cargo-cache:/usr/local/cargo/registry \
     delfin-dev \
     bash -lc "cd /workspace && cargo build --release"
   ```

### Native (host)
Install the native GTK/GLib stack and friends (Ubuntu/Mint):
```
sudo apt-get install -y \
  pkg-config libglib2.0-dev libglib2.0-bin \
  libgtk-4-dev libgdk-pixbuf-2.0-dev libcairo2-dev libpango1.0-dev libgraphene-1.0-dev \
  libadwaita-1-dev \
  libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev \
  libepoxy-dev libmpv-dev
```
Then build with `cargo build`.

### Optional
- Install pre-commit hooks with `pre-commit install`
- Use `mold` linker for faster builds if available.

### Flatpak packaging (Meson)
Meson files remain for Flatpak builds. To produce a Flatpak bundle:
```
meson setup -Dprofile=release -Dflatpak=true build-dist
meson dist -C build-dist
```
See `build-aux/cafe.avery.Delfin.Devel.yaml` and `build-aux/build-flatpak-dist` for the packaging flow.

## Translations

Translations will be re-opened once I figure out the best way to open that out to the community.
