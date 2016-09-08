# Spotifyd-http

This web server remote controls Spotify Connect devices via HTTP requests.

## Building
Rust 1.7.0 or later is required to build librespot.

It also requires a C and C++ toolchain, with libprotoc and portaudio.

On debian / ubuntu, the following command will install these dependencies :
```shell
sudo apt-get install build-essential portaudio19-dev libprotoc-dev
```

On Fedora systems, the following command will install these dependencies :
```shell
sudo dnf install portaudio-devel protobuf-devel make gcc gcc-c++
```

On OS X, using homebrew :
```shell
brew install portaudio protobuf
```

Once you've cloned this repository you can build *spotifyd-http* using `cargo`.
```shell
cargo build --release
```

## Usage
```shell
target/release/spotifyd_http --cache CACHEDIR --name NAME
```

## Methods

These are the currently supported methods:

### GET /devices
Returns a list of device ID/Name pairs.

### PUT /device_id/{play, pause, next, prev}
Plays, pauses, skips, and returns to previous song.

### {GET, PUT, POST} /device_id/tracks
Gets, replaces, or appends tracks to the playlist. The `PUT` and `POST` take
one or more `id` parameters. Example:
```bash
TRACKS="id=2BhU0Hl5OatWiCW93pE2b8&id=731OW49heGHCMrMOREHYlY&id=6zAPaRDoT99ThFtIXUJwhO"
curl -X POST -d "$TRACKS" 127.0.0.1:6767/device_id/tracs
```
