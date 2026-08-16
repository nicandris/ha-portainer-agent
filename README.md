# HA Add-ons (nicandris)

> **Cherry-picked from upstream.** The `portainer_agent` add-on in this repo is a copy of
> [alexbelgium/hassio-addons](https://github.com/alexbelgium/hassio-addons/tree/master/portainer_agent),
> taken as a single-commit snapshot with no upstream git history. Only that one add-on was copied —
> nothing else from that repo.

## Add-ons

| Add-on | Description |
|---|---|
| [Portainer Agent](portainer_agent) | Exposes this Home Assistant host's Docker to a remote Portainer instance. |

## Install

Home Assistant → Settings → Add-ons → Add-on Store → ⋮ → Repositories → add:

```
https://github.com/nicandris/ha-portainer-agent
```

Then install **Portainer Agent** and point Portainer at `<ha-host>:9001`.

> **Note:** this repo is private. The Supervisor clones add-on repositories anonymously, so it
> cannot read a private repo — make it public, or install the add-on by copying the folder into
> `/addons` on the HA host as a local add-on.

## Upstream

The add-on pulls the prebuilt image `ghcr.io/alexbelgium/portainer_agent-{arch}`; it does not build
the agent from source. To pick up upstream fixes, re-copy the folder from alexbelgium's repo.
