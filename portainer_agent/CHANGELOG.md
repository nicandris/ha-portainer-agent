# Changelog

## 2.45.3

- Portainer agent `2.45.2` → `2.45.3` (security: Go 1.26.10 with two Critical CVE fixes, golang.org/x/net
  0.60.0; eMudhra emSign roots removed from the CA bundle, so registries or Git hosts on emSign
  certificates stop working; [release notes](https://github.com/portainer/portainer/releases/tag/2.45.3)).
- Home Assistant base image `21.0.8` → `21.0.9`: Alpine `3.24.3`, musl `1.2.6-r3`
  ([app-base releases](https://github.com/hassio-addons/app-base/releases)).

## 2.45.2

- Portainer agent `2.45.1` → `2.45.2` (security: in-cluster Kubernetes API connections now verify
  TLS during stack deploy and removal, on the agent too;
  [release notes](https://github.com/portainer/portainer/releases/tag/2.45.2)).
- Home Assistant base image `21.0.7` → `21.0.8`: tzdata `2026e-r0`
  ([app-base releases](https://github.com/hassio-addons/app-base/releases)).

## 2.45.1.1

- Home Assistant base image `21.0.5` → `21.0.7`: Alpine `3.24.2`, tzdata `2026d-r0`,
  OpenSSL `3.5.9-r0` ([app-base releases](https://github.com/hassio-addons/app-base/releases)).
  The Portainer agent itself is unchanged at `2.45.1`.

## 2.45.1

- Portainer agent `2.45.0` → `2.45.1` (patch: SSRF hardening for Helm/Git requests,
  [release notes](https://github.com/portainer/portainer/releases/tag/2.45.1)).
- Home Assistant base image `21.0.4` → `21.0.5`: xz `5.8.4-r0`
  ([app-base releases](https://github.com/hassio-addons/app-base/releases)).

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
