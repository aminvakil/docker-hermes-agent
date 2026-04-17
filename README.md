# docker-hermes-agent

Automated daily Docker builds of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent), pushed to Quay.

This repository does not maintain its own Dockerfile. Instead, GitHub Actions checks out the upstream Hermes Agent repository and builds the upstream `Dockerfile` directly.

## Images

Built daily from upstream. Tags you may see include:

- `quay.io/aminvakil/hermes-agent:latest` — whichever upstream `main` commit was most recently built
- `quay.io/aminvakil/hermes-agent:<full-commit-sha>` — the exact upstream `main` commit built in a given run
- `quay.io/aminvakil/hermes-agent:<release-tag>` — the upstream latest release tag built in a given run, for example `v2026.4.16`

## Usage

Basic smoke test:

```bash
docker run --rm quay.io/aminvakil/hermes-agent:latest --help
```

Interactive run with persistent data:

```bash
docker run --rm -it \
  -v hermes-data:/opt/data \
  quay.io/aminvakil/hermes-agent:latest
```

If you want the container user to match your host UID/GID:

```bash
docker run --rm -it \
  -e HERMES_UID="$(id -u)" \
  -e HERMES_GID="$(id -g)" \
  -v hermes-data:/opt/data \
  quay.io/aminvakil/hermes-agent:latest
```

## Notes

- This repository rebuilds the current upstream `main` commit and current upstream latest release on a schedule.
- It is not a full archive and does not mirror every upstream commit or every historical release tag.
- `latest` tracks upstream `main`, not the latest tagged release.
- Release tags are preserved exactly as published by Hermes Agent upstream.
- Runtime behavior, entrypoint, and dependencies come from the upstream Hermes Agent Docker image definition.

## Upstream

- Upstream project: <https://github.com/NousResearch/hermes-agent>
- Upstream docs: <https://hermes-agent.nousresearch.com/docs/>
