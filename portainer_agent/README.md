# Portainer Agent

Runs the [Portainer agent](https://docs.portainer.io) on this Home Assistant host, so a remote
Portainer instance can manage the host's Docker containers, images, volumes and networks.

## What it is

A thin add-on wrapper: the agent binary is copied from the official `portainer/agent` image
(the tag pinned in the `Dockerfile`, which the add-on version tracks) onto the current Home Assistant base image, and started by s6-overlay. Nothing is built
from source and no third-party image is pulled at runtime.

## Configuration

Connect Portainer to `<home-assistant-host>:9001` as an **Agent** environment. No configuration
is required for that.

`env_vars` passes environment variables straight to the agent, for anything else it supports:

```yaml
env_vars:
  - name: AGENT_SECRET
    value: some-shared-secret
  - name: LOG_LEVEL
    value: DEBUG
```

Edge agent setups work the same way — set `EDGE`, `EDGE_ID` and `EDGE_KEY` as `env_vars`.
See the [agent environment variables](https://docs.portainer.io/admin/environments/add/docker/agent).

## Security

Anyone who can reach port 9001 can control the host's Docker — on Home Assistant OS that is
the whole system. Never expose the port to the internet, and set `AGENT_SECRET` (the same value
as `AGENT_SECRET` on the Portainer server) so the agent only accepts that Portainer instance.

## Updating

New agent releases ship as add-on updates through the Add-on Store. Maintainers: bump the tag in
`Dockerfile` **and** `version` in `config.yaml` — Dependabot only bumps the tag, and Home
Assistant offers an update only when `version` changes.

## Notes

- `docker_api` and `full_access` are required — the agent talks to the host Docker socket.
- Port 9001 is published. The edge agent does not need an inbound port.
