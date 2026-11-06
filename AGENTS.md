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

### Rulings

(none yet)

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

| Folder | What it is | Commands |
| ------ | ---------- | -------- |
| .      |            |          |

## Practices

Project practices (commit style, test commands, docs) go here.
