# Portainer Agent

Runs the official [Portainer agent](https://docs.portainer.io/admin/environments/add/docker/agent)
on this Home Assistant host, so a Portainer server elsewhere can manage the host's Docker
containers, images, volumes and networks.

The agent binary is copied from the `portainer/agent` image at the tag pinned in the
`Dockerfile`, and the add-on version tracks it. Nothing is built from source and no third-party
image is pulled at runtime.

**Set `AGENT_SECRET` before you rely on this add-on.** Without it, the agent trusts the first
Portainer server that reaches port 9001, and that server gets full control of this host. See
[AGENT_SECRET](#agent_secret) below.

## Connecting Portainer

In Portainer: **Environments → Add environment → Docker Standalone → Agent**, with environment
address `<home-assistant-host>:9001`. That works with no configuration, but set `AGENT_SECRET`
(below) before you rely on it.

## Configuration

`env_vars` passes environment variables straight to the agent, so any
[agent variable](https://docs.portainer.io/admin/environments/add/docker/agent) can be set:

```yaml
env_vars:
  - name: AGENT_SECRET
    value: 3f9c…d41a
  - name: LOG_LEVEL
    value: DEBUG
```

`name` must be letters, digits and underscores. Restart the add-on after changing it.

### AGENT_SECRET

Without a secret, the agent trusts the first Portainer server that connects to it. With one, it
accepts only a server holding the same secret. Set it on **both** sides:

1. Generate a value, e.g. `openssl rand -hex 32`.
2. **Portainer server:** add it as an environment variable on the Portainer container and
   recreate it. With Compose, put `AGENT_SECRET=<value>` in an env file next to the compose file
   and reference it with `env_file:`.
3. **This add-on:** add an `env_vars` entry with `name: AGENT_SECRET` and `value: <value>`, then
   restart the add-on.

The server sends its secret to **every** agent environment it manages, so all your other agents
need the same value too. Environments that use the local Docker socket are unaffected.

### Edge agent

Set `EDGE=1`, `EDGE_ID` and `EDGE_KEY` as `env_vars`, using the values Portainer shows when you
add an Edge environment. An Edge agent connects out to the server and needs no inbound port.

## Troubleshooting

**The environment shows `unauthorized`.** The agent and the server have different secrets, or
only one side has one. The usual mistakes:

- The whole line `AGENT_SECRET=<value>` was pasted into `value`, instead of just `<value>`.
- Stray quotes or spaces around the value.
- The add-on or the Portainer container was not restarted after the change.

To check the server's copy without showing it, run
`docker exec portainer printenv AGENT_SECRET | wc -c`: a 64-character hex secret prints `65`.

**Portainer still shows the old agent version after an update.** The Environments list shows
the version from the last snapshot. Refresh the environment, and trust the add-on log line
`App version:` over the Portainer UI.

**No update offered after a new release.** Open **Add-on Store → ⋮ → Check for updates** to make
the Supervisor fetch the repository again.

## Notes

- `docker_api` and `full_access` are required, because the agent talks to the host Docker
  socket. That is also why protection mode is off.
- Port 9001 is published. Keep it off the internet.
