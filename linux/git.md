---
title: Git
date-modified: 2023-08-30
---

## List authors and the number of commits

```shell
git shortlog --summary --email --numbered
```

## List authors in all branches

```shell
git shortlog -sne --all
```

## ignore file

to keep file in history but dont track changes:

```
git update-index --assume-unchanged FILE_NAME
```

and if you want to track the changes again use this command:

```
git update-index --no-assume-unchanged FILE_NAME
```

## checkout remote PR locally

Works on github

```
git fetch origin pull/ID/head:BRANCHNAME
```

## remove last commit

```
git reset --hard HEAD^
```

## remove multiple commits from top

```
git reset --hard HEAD~2
```

where `2` is the number of commits to remove

## Rename your local branch.

If you are on the branch you want to rename:

```
git branch -m new-name
```

If you are on a different branch:

```
git branch -m old-name new-name
```

## Delete the old-name remote branch and push the new-name local branch.

```
git push origin old-name new-name
```

## Reset the upstream branch for the new-name local branch.

Switch to the branch and then:

```
git push origin -u new-name
```

## patch/apply

1. Generate the patch:
   `diff old new > changes.patch`
   or
   `git diff > some-changes.patch`

2. Apply the diff:
   `git apply /path/to/some-changes.patch`

And that’s it! The changes are now in your working copy and ready to be staged/commit/pushed :)

## create patch from multiple commits

```
git format-patch cc1dde0dd^..6de6d4b06 --stdout > foo.patch
```

then to apply it

```
git am foo.patch
```

## last three commits

```
git format-patch -3 --stdout > multi_commit.patch
```

## all commits that are in your branch and not in master into a single patch file multi_commit.patch

```
git format-patch --signoff master --stdout > multi_commit.patch
```

## create patches in the folder ~/output/directory/ for all commits that are in your branch and not in master

```
git format-patch -o ~/output/directory/ --signoff master
```

## list only untracked files/directories

`git ls-files --exclude-standard --others`

for use with `xargs`

`git ls-files -z -o --exclude-standard | xargs -0 git add`

## delete untracked files

:remove:

```
git ls-files -z -o --exclude-standard | xargs -0 rm
```

## checkout at specific date

```
git checkout "`git rev-list master  -n 1 --first-parent --before=2008-03-02`"
```

## unshallow a clone

The below command will convert the shallow clone to regular one

```
git fetch --unshallow
```

Then, to get access to all the branches on origin

```
git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"
git fetch origin
```

## reset diverged master to origin

```
git reset --hard origin/master
```

## revert last n commits

from https://stackoverflow.com/a/43081965/10622119

`git revert --no-commit HEAD~3..`
This command reverts last 3 commits with only one commit.

Also doesn't rewrite history.

The `..` helps create a range. Meaning `HEAD~3..` is the same as `HEAD~3..HEAD`

## rebase

:squash:

`git rebase -i <after-this-commit>`
replace "pick" on the second and subsequent commits with "squash" or "fixup", as described in the manual.

## git diff show only filenames

`--name-only`

## visualize git commits

use `gource`

```
gource . -1920x1080 -s 0.01 --max-user-speed 300 --dir-name-depth 1 --highlight-users --disable-input --bloom-intensity 0.1 --bloom-multiplier 0.1 --filename-time 2 --hide filenames --date-format "%b %d %Y" -o - | ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i - -vcodec libx264 -preset ultrafast -pix_fmt yuv420p -crf 1 -threads 0 -bf 0 gource.mp4
```

## git diff: show lines added/removed

Use `--numstat`:

```sh
git diff --numstat
```

## show files that were changed in the last 2 days

```
git log --pretty=format: --name-only --since="2 days ago"
```

## search for commit content

To search for commit content (i.e., actual lines of source, as opposed to commit messages and the like), you need to do:

```
git grep <regexp> $(git rev-list --all)
```

```
git rev-list --all | xargs git grep <expression>
```

this will work if you run into an "Argument list too long" error.

## fetch and checkout remote branch

```
git fetch <remote-repository>
```

This fetch command will fetch all remote branches and also store all references/objects.
Then, checkout to the branch, giving you a local working copy.

```
git checkout -b <local-branch> <remote-repository>/<remote-branch>
```

or

```
git branch <local-branch> <remote-repository>/<remote-branch>
```

## debug `.gitignore`

Use `git check-ignore`:

```bash
git check-ignore [<options>] <pathname>...
git check-ignore [<options>] --stdin
```

## extract folder with history

You'll need [git-filter-repo](https://github.com/newren/git-filter-repo) for this.

On arch it's just `yay git-filter-repo`

```
git filter-repo --path folder --to-subdirectory-filter new-folder
```

This will:

1. Remove everything that is not in `folder`
2. Move everything that is in `folder` to `new-folder`
3. Keep git history of files in `folder`

## find first git commit

```
git rev-list --max-parents=0 HEAD
```
