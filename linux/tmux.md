---
title: Tmux
date-modified: 2022-07-12
---

Below `prefix` is mentioned multiple times. By default it is `<C-b>` which is `ctrl` + `b`.

It can be remapped to other key, i like to use `ctrl` + `a`:

```
set -g prefix C-a
```

## Detach from specific session

You can choose which session to detach with `prefix` + `D` (uppercase `D`)

## List all key bindings

```
tmux list-keys
```

or within tmux

```
:list-keys
```

or

```
`prefix` + `?`
```

## Kill window

`prefix` + `&`

## Kill pane

`prefix` + `x`

## Change color of one pane

```
select-pane -t:.1 -P 'fg=red,bg=white'
```

# Extract current pane into new window

`prefix` + `!`

# Move pane to somewhere else

1. go to pane you want to move
2. mark it with `prefix + m`
3. go to destination window/session
4. `:join-pane`

# Disable status bar

ctrl+a
set -g status off

---


