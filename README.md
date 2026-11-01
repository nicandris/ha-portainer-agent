# HA Add-ons (nicandris)

Home Assistant add-on repository.

| Add-on | Version | Description |
|---|---|---|
| [Portainer Agent](portainer_agent) | 2.45.3.1 | Exposes this host's Docker to a remote Portainer instance. |

## Install

Settings → Add-ons → Add-on Store → ⋮ → Repositories → add:

```
https://github.com/nicandris/ha-portainer-agent
```

Then install **Portainer Agent** — it builds on the host — and add it to Portainer as an
**Agent** environment at `<ha-host>:9001`.

> **Security:** the agent gives whoever reaches port 9001 full control of the host's Docker,
> which on Home Assistant OS means the whole system. Keep the port off the internet and set
> `AGENT_SECRET` — see the [add-on docs](portainer_agent/README.md).

## Origin

The `portainer_agent` add-on started as a copy of
[alexbelgium/hassio-addons](https://github.com/alexbelgium/hassio-addons/tree/master/portainer_agent)
and has since been rewritten: it now builds from the official `portainer/agent` image on the
current Home Assistant base, with no dependency on that repository's build machinery or prebuilt
images. See [`portainer_agent/CHANGELOG.md`](portainer_agent/CHANGELOG.md).
