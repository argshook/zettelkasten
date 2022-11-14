---
title: Tig
date-modified: 2022-11-14
---

## Advanced filtering

Just, pipe `git log` right into `tig`, for example:

```
git log --author="Name Surname" | tig
```

## View revisions of file

Use `blame`
* `vt` to open tree view of commit
* navigate to file with hjkl and enter
* `b` to open `blame` view
* `b` again to step backwards of a given line
* `,` to step backwards to the parent commit of a given line
* `<` to return to where you were previously

