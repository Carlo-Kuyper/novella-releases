# Novella — downloads

Pre-built binaries for [Novella](https://github.com/pixelated-digital-studio), a
self-hosted audiobook and ebook library. **This repo has no source code in
it on purpose** — it only holds built releases published automatically by
CI from the (private) source repo. Novella itself is free; this is just
where the downloads live.

## Get the server

The server is the whole app — it serves its own web UI, so this is the only
piece most people need. It's a single self-contained file: no installer, no
separate folder of assets, no `.env` to set up.

1. Go to [Releases](../../releases) and grab the file for your OS:
   - `novella-server-vX.Y.Z-windows-x86_64.exe`
   - `novella-server-vX.Y.Z-linux-x86_64` (run `chmod +x` on it first)
   - `novella-server-vX.Y.Z-macos-aarch64` (Apple Silicon; `chmod +x` first)
2. Put it wherever you want it to live permanently, then run it. It creates
   a `data/` folder next to itself on first run (the SQLite database), so
   don't run it straight out of Downloads/temp.

   **Windows**: it's unsigned (no code-signing certificate yet), so
   SmartScreen will likely show a "Windows protected your PC" warning —
   click **More info → Run anyway**. If you dismiss that warning instead,
   the server never actually starts (nothing in Task Manager, nothing
   listening on the port) — that's SmartScreen blocking it, not a broken
   download. It doesn't install anything or show up in Control Panel/Apps
   either — it's a plain executable you run directly, like `curl.exe`.
3. Open `http://localhost:8080` and log in with `root` / `admin` (you'll be
   asked to change the password immediately).

**Windows**: while it's running, look for a Novella icon in the system
tray (bottom-right, near the clock) — right-click for Open/Quit. If you
don't see it right after starting it, check the **^** overflow arrow next
to the tray — Windows often hides a brand-new icon there until you drag it
out or Windows "learns" to keep it visible; that's normal Windows
behavior, not a bug.

Want it running in the background / on boot instead of a terminal window?
See [`service-setup/`](service-setup) in this repo for systemd (Linux),
launchd (macOS), and Task Scheduler (Windows) templates — one set, reused
across every version, since they don't change per release.

### Or run it with Docker

```bash
docker run -d \
  --name novella \
  -p 8080:8080 \
  -v novella-data:/app/data \
  ghcr.io/pixelated-digital-studio/novella:latest
```

Or pin a specific version instead of `latest`: check the
[Releases](../../releases) page for available version tags.

## Get the desktop app

A native window that connects to a Novella server you already have running
(it does **not** bundle its own server). Windows/macOS/Linux installers are
attached to each [release](../../releases):

- Windows: `novella-desktop-vX.Y.Z-windows-x86_64.msi` or
  `novella-desktop-vX.Y.Z-windows-x86_64-setup.exe`
- macOS: `novella-desktop-vX.Y.Z-macos-aarch64.dmg`
- Linux: `novella-desktop-vX.Y.Z-linux-x86_64.deb` or
  `novella-desktop-vX.Y.Z-linux-x86_64.AppImage`

These installers are currently **unsigned** — expect a SmartScreen
(Windows) or Gatekeeper (macOS) warning on first run. That's expected for
now, not a sign of a bad download; verify against `SHA256SUMS.txt` on the
release if you want to double check.

## Mobile app

Not published here yet — coming in a future update. When it lands it'll
follow the same naming pattern as everything else:
`novella-mobile-vX.Y.Z-android.apk` and `novella-mobile-vX.Y.Z-ios.ipa`.

## Verifying a download

Every release includes a `SHA256SUMS.txt`. Verify with:

```bash
sha256sum -c SHA256SUMS.txt --ignore-missing
```

## Reporting an issue

Use this repo's [Issues](../../issues) tab — reports and download problems
only; there's no source here to open pull requests against.
