# Running Novella on boot (Windows)

No custom Windows service wrapper is shipped yet — the simplest reliable
option today is a Task Scheduler task that starts on boot and restarts on
failure:

1. Put the downloaded `novella-server-vX.Y.Z-windows-x86_64.exe` somewhere
   permanent, e.g. `C:\Novella\server.exe` (it's a single self-contained
   file — no separate `web\` folder or `.env` needed alongside it).
2. Open **Task Scheduler** -> **Create Task...** (not "Basic Task", so you
   get the restart-on-failure option).
3. **General** tab:
   - Name: `Novella`
   - "Run whether user is logged on or not"
   - "Run with highest privileges" (only needed if binding to a low port;
     not required for the default `0.0.0.0:3939`)
4. **Triggers** tab -> New -> "At startup".
5. **Actions** tab -> New -> Start a program:
   - Program/script: `C:\Novella\server.exe`
   - Start in (this matters — it's where the `data\` folder, holding the
     database, gets created): `C:\Novella`
6. **Settings** tab:
   - "If the task fails, restart every" 1 minute, up to 3 times (or more)
   - "If the running task does not end when requested, force it to stop"
7. Save, then right-click the task -> Run, and check
   `http://localhost:3939` loads.

Logs go to stdout only today (no file logging) — run `server.exe` from a
terminal instead of via Task Scheduler if you need to watch logs live.
