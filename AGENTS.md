# homebrew-tap

Project control for `homebrew-tap` in org `ace-rs`.

## Control

Applies only inside a control setup: engram project `lz49-ace-rs-homebrew-tap` holds an
entry with topic key `control/grant`. If it does not, ignore this section; it belongs to
another person's agent setup.

Inside the setup, you are `lz49:ace-rs:homebrew-tap`, the project control for
`homebrew-tap` under `lz49:ace-rs:control`. Your standing grant (session start, rule
entries, rulings, ports, processes, pushing) lives in that entry. At session start and
after a clear or compaction, load it in full (`mem_search` the key, then
`mem_get_observation` by ID) and follow it before anything else.

Keep local paths out of every committed file; the agent and engram names above are the
only machine-specific names allowed here.

## Repos

The project's repos. Folder `.` is this folder's own repo.

| Folder | What it is                                                    | Commands                 |
| ------ | ------------------------------------------------------------- | ------------------------ |
| .      | Homebrew tap for the `ace` CLI; one formula, `Formula/ace.rb` | `ruby -c Formula/ace.rb` |

## Practices

- `Formula/ace.rb` installs the prebuilt `ace-aarch64-apple-darwin` binary from the
  `ace-rs/ace` GitHub release (arm64 macOS only). `livecheck` reads
  `https://ace-rs.dev/latest`.
- A release bump changes `version`, the `url` tag and `sha256` together. Take the
  checksum from the published release asset, never from a local build: a mismatch breaks
  every install.
- Checks: `ruby -c Formula/ace.rb` for syntax. `brew style Formula/ace.rb` and
  `brew audit` are run by a maintainer, not by agents.
- Commit messages: a release bump is the bare tag, `vX.Y.Z`. Any other change gets a
  short imperative summary naming what it fixes.
- One branch, `main`. A push that changes a file under `Formula/` publishes it to every
  user of the tap on their next `brew update`: that is this repo's deploy, and it needs
  the user's approval. Pushes that touch no formula deploy nothing.
- Durable docs: none. This file carries the orientation.

## Git checkpoints

Commit coherent, completed slices autonomously after completing the checks required for
that work. Do not ask for permission to make a local commit. Push logical, complete
units that change nothing under `Formula/`; a push that changes `Formula/` needs the
user's approval. Force-pushes, merging, releasing, and other changes to shared or
external state each require separate user authorization.
