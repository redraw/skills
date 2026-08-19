# Building and Deploying CircuitJS1

Source: [pfalstad/circuitjs1 README](https://github.com/pfalstad/circuitjs1). This covers running your **own instance** of the simulator (as opposed to the file format itself — see [text-format.md](text-format.md) / [xml-format.md](xml-format.md) for that).

## Build toolchains

| Method | Summary |
|---|---|
| **Eclipse** | "Eclipse for Java developers" + GWT Eclipse plugin. Run in GWT super dev mode via the toolbar, or "GWT Compile Project..." to build for deployment. Output goes to `war/`. |
| **Cloud dev container** (Codespaces / Gitpod) | Open the fork in a dev container via VS Code's remote extension, then inside it: `./dev.sh setup` (installs GWT/Java), `./dev.sh start` (serves on `:8000`, code server on `:9876`). Requires forwarding both ports; use the local VS Code desktop app, not the browser-based editor (port-forwarding on Gitpod/Codespaces maps to hostnames, which confuses the GWT code loader). |
| **Gradle** | `gradle compileGwt --console verbose --info` then `gradle makeSite --console verbose --info`, producing `site/circuitjs.html`. Serve with `cd site && python3 -m http.server`. Requires **Gradle 8.7** specifically — the GWT plugin is incompatible with Gradle 9.x. |
| **Quick local test** | `./test.sh` (or `./test.sh 9000` for a custom port) — compiles, builds the site, and serves it, opening the browser automatically on macOS. Needs Python 3. |

## Docker / Podman

```bash
# production image
podman build -f circuitjs1.Containerfile -t circuitjs1:latest
podman run --name=circuitjs1 --rm -d -p 8000:8000 circuitjs1:latest
# → http://localhost:8000/circuitjs.html

# development image (live-editable via bind mount)
podman build -f dev-start.Containerfile -t circuitjs1-dev:latest
podman run --rm -it -v $(pwd):/src:Z -p 127.0.0.1:8000:8000/tcp -p 127.0.0.1:9876:9876/tcp circuitjs1-dev:latest
```
(swap `podman` for `docker` if preferred)

## Deploying the compiled app

1. GWT-compile (`./dev.sh compile` or the Eclipse GWT compile step) — output lands in `war/`.
2. Copy everything in `war/` **except** `WEB-INF/` to your web server.
3. Customize `circuitjs1.html`'s `<head>` for analytics/favicon/etc.
4. Customize `iframe.html` — it's loaded as an iframe in the spare space at the bottom of the right-hand panel, useful for branding.
5. `shortrelay.php` is an optional server-side relay for a URL-shortening service, avoiding cross-origin issues with a purely client-side approach. Customize it, or if unused, remove the feature by editing `circuitjs1.java` before compiling.
6. To enable Dropbox load/save, add a Dropbox API app-key into `circuitjs.html`. Without it, that feature is simply disabled.

Expected file layout for a deployed site:
```
<front-page dir>/
  circuitjs.html         # full-page app entry point (can be renamed — update shortrelay.php too)
  iframe.html            # branding panel, see above
  shortrelay.php         # optional URL-shortener relay
  circuitjs1/            # GWT build output
    circuits/            # example circuit files
    setuplist.txt         # index into circuits/
```

The public entry point is `http://<host>/<path>/circuitjs1.html`.

## Electron desktop build

See [embedding.md](embedding.md#building-an-electron-desktop-app).
