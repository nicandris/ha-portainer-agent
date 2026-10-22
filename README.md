# HA Add-ons (nicandris)

Private Home Assistant add-on repository.

| Add-on | Version | Description |
|---|---|---|
| [Portainer Agent](portainer_agent) | 2.45.3 | Exposes this host's Docker to a remote Portainer instance. |

## Install

This repository is **private**. Add it with a GitHub token embedded in the URL:

Settings → Add-ons → Add-on Store → ⋮ → Repositories → add:

```
https://<TOKEN>@github.com/nicandris/ha-portainer-agent
```

Use a fine-grained personal access token scoped to this repository with **Contents: read-only**.
The Supervisor passes the URL straight to `git clone`, so the credentials just work.

Then install **Portainer Agent** — it builds on the host — and point Portainer at
`<ha-host>:9001`.

> **The token is stored in plaintext** in the Supervisor's store config and is visible in the
> repository list in the UI. Scope it to read-only on this one repo, and rotate it if the HA
> config is ever shared or backed up somewhere untrusted.

Alternatively, skip the token and install it as a local add-on:

```bash
# on the Home Assistant host
git clone https://github.com/nicandris/ha-portainer-agent /addons/ha-portainer-agent
```

## Origin

The `portainer_agent` add-on started as a copy of
[alexbelgium/hassio-addons](https://github.com/alexbelgium/hassio-addons/tree/master/portainer_agent)
and has since been rewritten: it now builds from the official `portainer/agent` image on the
current Home Assistant base, with no dependency on that repository's build machinery or prebuilt
images. See `portainer_agent/CHANGELOG.md`.
