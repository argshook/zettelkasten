---
title: Tmux
date-modified: 2021-11-29
---

# Tmux

To kill the current session hit subsequently `Enter` + `~` + `.`

To choose which session to detach use `prefix` + `D` (uppercase D)

```
# list all key bindings
tmux list-keys

# or within tmux
:list-keys

# or within tmux
?
```

kill window `Prefix` + `&`
kill pane `prefix` + `x`

change color of one pane

```
select-pane -t:.1 -P 'fg=red,bg=white'
```

# split (extract) current pane into new window

`prefix !`, so `c-a !` :)

# move pane to whereverr

1. go to pane you want to move
2. mark it with `prefix + m`
3. go to destination window/session
4. `:join-pane`

# disable status bar

ctrl+a
set -g status off
