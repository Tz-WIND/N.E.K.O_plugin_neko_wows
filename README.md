# N.E.K.O World of Warships Companion

`neko_wows` is a read-only World of Warships companion plugin for N.E.K.O. It
consumes local `8111_for_wows` telemetry, turns frames into battle events, and
lets the active character deliver prioritized call-outs. It does not automate
game input or read game memory.

## Repository layout

- `neko_wows/`: runtime Python package, hosted UI, locales, and replay fixture
- `tests/`: plugin unit and replay tests
- `scripts/`: offline ship-catalog tooling
- `plugin.toml`: N.E.K.O plugin manifest and default configuration

## Development

Keep this repository next to an N.E.K.O checkout:

```text
workspace/
├── N.E.K.O/
└── N.E.K.O_plugin_neko_wows/
```

Until the required host capabilities merge upstream, use the
`Tz-WIND/N.E.K.O` branch `feat/plugin-host-capabilities`.

Run tests from this repository root:

```powershell
uv run --project ../N.E.K.O pytest -q
```

Validate and build the installable package with the host CLI:

```powershell
uv run --project ../N.E.K.O neko-plugin check -r .
uv run --project ../N.E.K.O neko-plugin build .
```

The generated package is not published automatically. Publishing requires an
explicit version tag or manual workflow invocation.

## Ship catalog

Build an immutable offline catalog with a pinned `wowsinfo/data` commit:

```powershell
uv run --project ../N.E.K.O python scripts/build_neko_wows_ship_catalog.py `
  --revision <40-character-commit-sha> `
  --output-dir <plugin-data-directory>/ship_catalog
```

## License

Apache License 2.0. See `LICENSE`.
