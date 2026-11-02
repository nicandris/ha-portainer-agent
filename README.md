# Portainer Agent — Home Assistant add-on

[![CI](https://github.com/nicandris/ha-portainer-agent/actions/workflows/ci.yaml/badge.svg)](https://github.com/nicandris/ha-portainer-agent/actions/workflows/ci.yaml)
![Add-on version](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fraw.githubusercontent.com%2Fnicandris%2Fha-portainer-agent%2Fmain%2Fportainer_agent%2Fconfig.yaml&query=%24.version&label=add-on)
![Architectures](https://img.shields.io/badge/arch-amd64%20%7C%20aarch64-blue)

> [!WARNING]
> **No longer maintained (November 2026).** Portainer 3.0 has no Community Edition: CE is
> frozen on the 2.x line, with 2.45 LTS as its last release, and 3.x continues only as the
> closed-source Business Edition. I've moved my own setup off Portainer, so unfortunately I
> won't be maintaining this add-on any more, and the repository is archived. It keeps working
> as-is, but it won't get agent updates or fixes.

Run the official [Portainer agent](https://docs.portainer.io/admin/environments/add/docker/agent)
on your Home Assistant OS / Supervised host, so the Portainer server you already run elsewhere can
manage the host's Docker containers, images, volumes and networks.

> [!IMPORTANT]
> **Set `AGENT_SECRET`.** Without it, the agent trusts the first Portainer server that reaches
> port 9001 — and that server gets full control of your Home Assistant host. Put the same value on
> the Portainer server and in this add-on's `env_vars`; only the value goes in the add-on field,
> not `AGENT_SECRET=…`. Steps: [add-on docs](portainer_agent/README.md#agent_secret).

- **Official binary, nothing else.** The agent is copied from the `portainer/agent` image at the
  tag pinned in [`Dockerfile`](portainer_agent/Dockerfile), onto the
  [Home Assistant base image](https://github.com/hassio-addons/app-base). No third-party image is
  pulled at runtime.
- **Versioned with the agent.** Add-on `3.0.0` ships agent `3.0.0`; a fourth component
  (`3.0.0.1`) marks a rebuild on a newer base image.
- **Any agent option.** Every
  [agent environment variable](https://docs.portainer.io/admin/environments/add/docker/agent) can
  be set from the add-on configuration, including `AGENT_SECRET` and the Edge agent variables.

## Installation

[![Add repository to my Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fnicandris%2Fha-portainer-agent)

Or by hand: **Settings → Add-ons → Add-on Store → ⋮ → Repositories**, add

```
https://github.com/nicandris/ha-portainer-agent
```

Then:

1. Install **Portainer Agent**. It builds on the host, so the first install takes a minute.
2. Start it.
3. In Portainer: **Environments → Add environment → Docker Standalone → Agent**, with
   environment address `<home-assistant-host>:9001`.

## Security

The agent gives whoever reaches port 9001 full control of the host's Docker, which on Home
Assistant OS means the whole system. Never forward the port to the internet, and set a shared
`AGENT_SECRET` so the agent accepts only your Portainer server. The
[add-on documentation](portainer_agent/README.md#agent_secret) has the steps.

## Documentation

Configuration, `AGENT_SECRET` setup, Edge agents and troubleshooting:
[`portainer_agent/README.md`](portainer_agent/README.md). The same page is shown on the add-on's
Info tab in Home Assistant.

Release notes: [`portainer_agent/CHANGELOG.md`](portainer_agent/CHANGELOG.md).

## Development

CI lints the add-on config and builds both architectures on every push and pull request.
Dependabot watches the agent image and the GitHub Actions.

To release a new agent version, bump **both**:

- the `portainer/agent` tag in `portainer_agent/Dockerfile`, and
- `version` in `portainer_agent/config.yaml`, plus a `CHANGELOG.md` entry.

Dependabot bumps only the tag, and Home Assistant offers an update only when `version` changes.
The Home Assistant base image is pinned in `portainer_agent/build.yaml`, which Dependabot cannot
read, so bump it by hand and release it as a fourth-component version.

## Credits

Started from the `portainer_agent` add-on in
[alexbelgium/hassio-addons](https://github.com/alexbelgium/hassio-addons/tree/master/portainer_agent),
since rewritten to build from the official image without that repository's build machinery.

## License

[MIT](LICENSE)
