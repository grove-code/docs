# grove

A lean architecture for the multiplayer grove **server** — a single Phoenix app
(API + LiveView) over a Rust core (CLI + git/manifest mutations), with files
(`manifest.toml` + git) as the only source of truth.

## Install

```sh
curl -fsSL https://grove-code.dev/install.sh | bash
grove on        # start the local server (127.0.0.1:7777)
```

- Spec: [`docs/overview.md`](docs/overview.md)
- Build plan: [`docs/quest.md`](docs/quest.md)

## Layout

```
apps/grove/    # Elixir/Phoenix server (API, LiveView, orchestration, observability)
crates/        # Rust workspace: grove (CLI + self-update) · grove-ops (git/manifest mutations)
               #   — pty/discover crates are planned (see docs/overview.md), not yet built
packages/ui/   # @grove/ui — React "view islands" the LiveViews mount
mise.toml      # pinned toolchain + tasks
legacy/        # frozen v3 tree — not built or released (see plans/promote-v1.md)
```

## Develop

```sh
mise run setup          # deps + build
mise run test           # ExUnit + cargo test
mise run check          # format + lint (read-only)
mise run fmt            # auto-format
mise run smoke          # hermetic install/update/rollback (CLI)
mise run release        # assemble a release bundle locally (CLI + server + grove-ops)
mise run smoke-release  # assemble + install + prove the released mutation layer is live
```
