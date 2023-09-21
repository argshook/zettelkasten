---
title: Vim
date-modified: 2023-07-18
---

## Move lines matching pattern to the bottom of file

```vim
:g/[pattern]/m $
```

### Example

I had a bash file with repeated patterns of:

```bash
_some_function () {
  # ...
}
alias some_function=_some_function

_another_function () {
  # ...
}
alias another_function=_another_function
```

Wanted to detach function declarations and aliases, so that file would look like:

```bash
_some_function () {
  # ...
}

_another_function () {
  # ...
}

alias some_function=_some_function
alias another_function=_another_function
```

I used the following command:

```vim
:g/^alias/m $
```

Function declarations remain untouched, while all aliases go down to the bottom of file.

The `:g[lobal]` command is neat! [`:help :global`](https://vimhelp.org/repeat.txt.html#%3Aglobal)

## Reverse order of lines

```vim
:g/^/m0
```
