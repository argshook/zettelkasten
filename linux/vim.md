---
title: Vim
date-modified: 2022-11-29
---

# Move lines matching pattern to the bottom of file

```
:g/[pattern]/m $
```

## Example

I had a bash file with repeated patterns of:

```
_some_function () {
...
}
alias some_function=_some_function
```

Wanted to detach function declaration and alias:

```
:g/^alias/m $
```

Function declarations remain untouched, while all aliases went down to bottom of file.

The `:g[lobal]` command is neat

[`:help :global`](https://vimhelp.org/repeat.txt.html#%3Aglobal)

## Reverse order of lines

```
:g/^/m0
```
