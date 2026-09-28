# Novella — downloads

Pre-built binaries for [Novella](https://github.com/Carlo-Kuyper), a
self-hosted audiobook and ebook library. **This repo has no source code in
it on purpose** — it only holds built releases published automatically by
CI from the (private) source repo. Novella itself is free; this is just
where the downloads live.

## Get the server

The server is the whole app — it serves its own web UI, so this is the only
piece most people need.

1. Go to [Releases](../../releases) and grab the archive for your OS:
   - `novella-vX.Y.Z-windows-x86_64.zip`
   - `novella-vX.Y.Z-linux-x86_64.tar.gz`
   - `novella-vX.Y.Z-macos-aarch64.tar.gz` (Apple Silicon)
2. Extract it, then run `server.exe` (Windows) or `./server`
   (macOS/Linux) from inside the extracted folder.
3. Open `http://localhost:8080` and log in with `root` / `admin` (you'll be
   asked to change the password immediately).

Each archive includes templates for running it as a background
service/daemon on boot (systemd/launchd/Task Scheduler) — see the
`README.txt` inside the archive.

### Or run it with Docker

```bash
docker run -d \
  --name novella \
  -p 8080:8080 \
  -v novella-data:/app/data \
  ghcr.io/carlo-kuyper/novella:latest
```

Or pin a specific version instead of `latest`: check the
[Releases](../../releases) page for available version tags.

## Get the desktop app

A native window that connects to a Novella server you already have running
(it does **not** bundle its own server). Windows/macOS/Linux installers are
attached to each [release](../../releases):

- Windows: `.msi` or `.exe`
- macOS: `.dmg`
- Linux: `.deb` or `.AppImage`

These installers are currently **unsigned** — expect a SmartScreen
(Windows) or Gatekeeper (macOS) warning on first run. That's expected for
now, not a sign of a bad download; verify against `SHA256SUMS.txt` on the
release if you want to double check.

## Mobile app

Not published here yet — coming in a future update.

## Verifying a download

Every release includes a `SHA256SUMS.txt`. Verify with:

```bash
sha256sum -c SHA256SUMS.txt --ignore-missing
```

## Reporting an issue

Use this repo's [Issues](../../issues) tab — reports and download problems
only; there's no source here to open pull requests against.
