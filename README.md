# Desktop Services

`@eduwork/desktop-services` · v0.1.0-dev.20260910.1 · MulanPSL-2.0 AND MIT

The desktop half of the DSH experience: a Host-only service that forwards authenticated requests to the EduWork shell for window attention, the desktop pet, update workbench actions, configuration file opening and external links, and that owns the shared notification preferences for the installation. Each call uses the bridge credential from `desktop-boundary`, never a renderer-supplied URL.

The package is meant for the desktop build only. A pure Web deployment has neither the bridge nor these endpoints.

## Highlights

- Host service `desktopServices` with no Remote decorator, so the renderer cannot choose an endpoint or read the bridge credential.
- Authenticated bridge calls to `POST /v1/extensions/attention`, `/v1/extensions/pet`, `/v1/extensions/workbench`, `/v1/extensions/open-configuration` and `/v1/desktop/open-external`.
- Workbench actions cover update status, checks, diagnostics, downloads, scheduling, installs, stable and development channels, content updates and the automatic-download and software-update switches.
- One shared preference set in the `eduwork-notifications` settings namespace (`enabled`, `attention`, `completed`, `failed`, `studio`, `sound`, `preview`), applied live.
- Plugin notification sources using protocol version 1 are bridged into the same attention transport, and Agent notifications keep working when no plugin registry is loaded.
- `openExternal` accepts only `http:` and `https:` URLs without embedded credentials.
- Per-request timeouts: 5 s for attention pushes, 10 s for the pet window, 15 s for opening a browser and 30 s for workbench actions.

## Install

Install this directory as a local DSH plugin bundle. From a shell:

```bash
dsh plugin --profile web add /absolute/path/to/desktop-services
```

Or add the directory through the **Plugins** panel in DSH (local bundle). Restart the DSH app after installation; plugins are activated from the bundle patch (`cordis.patch.yml`).

## Configuration

No configuration keys: the bundle patch inserts the plugin with defaults.

The plugin accepts a `notifications` object that seeds the `eduwork-notifications` settings namespace; the seven keys are booleans, with `enabled`, `attention`, `completed`, `failed` and `studio` defaulting to `true` and `sound` and `preview` to `false`.

## Requirements

- DeepSeek Harness >=0.2.1 <0.3.0
- Peer packages: @deepseek-ai/cordis, @deepseek-ai/schemastery, @deepseek-ai/dsh-settings, @deepseek-ai/dsh-session, @deepseek-ai/dsh-host-directory-picker

## Notes and limits

- Requires the authenticated desktop bridge (`desktopBoundary`) and the shell endpoints behind it; nothing works on a plain Web deployment.
- Only the package entry is reachable through `exports`: `lib/directory-picker.js` and `lib/workspace-access.js` ship in the tarball but are not imported by `lib/index.js` and are not exported as subpaths, so native directory picking and the Windows workspace-grant repair are not wired by this bundle as published.
- Attention is observe-only: it never answers, cancels or changes an agent's policy, it keeps at most 200 live items, and it truncates titles to 120 characters.
- Development-stage build: the version is `0.1.0-dev.20260910.1`.

## 中文文档

[README.zh-CN.md](./README.zh-CN.md)

## License

MulanPSL-2.0 AND MIT — see [LICENSE](./LICENSE) and, where present, [LICENSE-MIT](./LICENSE-MIT). Extracted from the ECNU EduWork distribution (https://github.com/ECNU/EduWork); upstream copyright and license notices are preserved.
