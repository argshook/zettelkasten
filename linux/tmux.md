---
title: Tmux
date-modified: 2023-01-04
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

## Extract current pane into new window

`prefix` + `!`

## Move pane to somewhere else

1. go to pane you want to move
2. mark it with `prefix + m`
3. go to destination window/session
4. `:join-pane`

## Disable status bar

1. Open command prompt with <kbd>prefix</kbd>+<kbd>:</kbd> (in my case prefix is <kbd>ctrl</kbd>+<kbd>a</kbd>, so full command is <kbd>ctrl</kbd>+<kbd>a</kbd>+<kbd>:</kbd>)
2. `set -g status off`

## split programatically

```
tmux split-window "echo hey"
```

This will work but close immediatelly after `echo`

To keep it open:

```
tmux set-option remain-on-exit on
tmux split-window "echo hey"
```
