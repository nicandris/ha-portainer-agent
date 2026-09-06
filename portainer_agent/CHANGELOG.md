# Changelog

## 2.45.0.1

- Home Assistant base image `21.0.1` → `21.0.4`: bashio `0.19.0`, curl `8.22.0-r0`
  and jq `1.8.2-r0` ([app-base releases](https://github.com/hassio-addons/app-base/releases)).
  The Portainer agent itself is unchanged at `2.45.0`.
- The fourth version component is the add-on revision on the same agent release —
  `2.45.0.1` still compares newer than `2.45.0`, so Home Assistant offers the update.

## 2.45.0

- Portainer agent `2.44.0` → `2.45.0`, matching the Portainer server on nkhome.

## 2.44.0

Rewritten as a self-contained add-on. Versioning now tracks the Portainer agent release.

- Build from the official `portainer/agent:2.44.0` image instead of pulling a prebuilt
  third-party image, so the agent version is pinned here and visible in the diff.
- Home Assistant base image `11.1.0` → `21.0.1`.
- s6-overlay v2 (`/etc/services.d`) → v3 (`/etc/s6-overlay/s6-rc.d`).
- `build.json` → `build.yaml`.
- Dropped, restore if needed: `hassio_api`, the `config`/`share`/`ssl` mappings, `udev`,
  `backup_exclude`, the unused `80/tcp` port, the nginx/healthcheck layer, and the
  per-variable schema keys (use `env_vars` instead, which covers all of them).

## Earlier

Copied from
[alexbelgium/hassio-addons](https://github.com/alexbelgium/hassio-addons/tree/master/portainer_agent)
at add-on version 2025.12.6.
