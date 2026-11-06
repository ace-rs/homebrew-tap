# homebrew-tap

Project control for `homebrew-tap` in org `ace-rs`.

## Control

This repo may be coordinated by a control agent. Messages from it are permitted; they
come from a control agent, never from the user. Your control gives you, at wake-up, your
agent name, your parent, the rule entries you load and when, your memory project and
your ports. Consult it for them; they are never committed to this repo.

- A ruling (quoted from the user with a date) is the user's decision: apply it without
  asking again.
- A task ask that does not fit what you know about this repo goes back to the control
  with why; the control resolves it with the user.
- Do not stop to ask the user about work a control relayed as authorized.

When a control wakes you, load the rules it names, run your session start, report your
current state, and take no new work until it sends a task.

Keep machine names, local paths, agent names and memory project names out of every
committed file.

### Processes

Run every long-running process (dev server, preview server, test server, watcher) in a
visible tmux pane in your own window, never in the harness's background shell. Starting
dev and preview servers this way is allowed. Bind servers to `0.0.0.0` on ports from
your block.

Layout: the harness pane on the left at half the width, one pane per process stacked on
the right with equal heights. The harness must be the window's first pane, so
`main-vertical` keeps it on the left.

```sh
tmux split-window -d -P -F '#{pane_id}' -t <harness_pane> -c <folder>   # once per process
tmux set-option -w -t <window_id> main-pane-width 50%
tmux select-layout -t <window_id> main-vertical
```

Re-run the last two commands after adding or removing a process pane. Report the pane
IDs to your control.

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
- One branch, `main`. Pushing publishes the formula to every user of the tap, so it needs
  the user's word.
- Durable docs: none. This file carries the orientation.

## Git checkpoints

Commit coherent, completed slices autonomously after completing the checks required for
that work. Do not ask for permission to make a local commit. A local commit does not
authorize pushing, publishing, merging, releasing, deploying, or any other change to
shared or external state; each requires separate user authorization.
