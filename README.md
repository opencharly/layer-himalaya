# himalaya

Himalaya email CLI layer for OpenCharly images.

The `himalaya` candy builds and installs the
[Himalaya](https://github.com/pimalaya/himalaya) email CLI from crates.io via
`cargo install himalaya`, run as the image user so the binary lands in the
user's cargo bin (`~/.cargo/bin`, which the required `rust` candy puts on
`PATH`).

Himalaya is a single self-contained Rust binary that speaks IMAP and SMTP to
manage accounts, folders, envelopes, and messages from the command line. The
install is verifiable at build scope: the binary is present, runs `--version`
cleanly, and its `--help` advertises the email-management subcommands.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `himalaya` |
| Requires | `layer-rust` |
| Binary | `${HOME}/.cargo/bin/himalaya` |
| Install files | `charly.yml` (`run:` step) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-himalaya:v2026.246.1950'
```

After the image is built:

```bash
~/.cargo/bin/himalaya --version
~/.cargo/bin/himalaya --help        # account, folder, envelope, message
```

Configure an IMAP/SMTP account (credentials via `charly secrets` —
`/charly-build:secrets`) to list folders and fetch envelopes.

## Layout

- `charly.yml` — the `himalaya:` candy entity: the `rust` require, the `run:`
  install step, the `check:` assertions, and the embedded `skill:` entity.
- `CHANGELOG/` — per-CalVer release notes.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:himalaya` — the IMAP/SMTP email CLI
- Runtime parent: `/charly-coder:rust`
- Pairs with: `/charly-infrastructure:gnupg` (PGP-encrypted email)
- Bundled by: `/charly-openclaw:openclaw-full` (metalayer)
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
