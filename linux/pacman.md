---
title: pacman
date-modified: 2024-09-03
---

## check how many cached packages are available

```shell
sudo ls /var/cache/pacman/pkg/ | wc -l
```

## check total disk space used

```shell
du -sh /var/cache/pacman/pkg/
```

## To clean all packages, except the 3 most recent versions:

```shell
sudo paccache -r
```

Paccache removed old and/or uninstalled packages from the cache.
check how many packages are left.

```shell
sudo ls /var/cache/pacman/pkg/ | wc -l
```

---

want to remove more packages? `paccache` allows to decide how many recent versions to keep.
command if you want to keep only one most recent version:

```shell
sudo paccache -rk 1
```

`k` - keep number of each package in the cache.

## To remove all cached versions of uninstalled packages:

```shell
sudo paccache -ruk0
```

`u` - the uninstalled packages.

## remove all uninstalled packages:

```shell
sudo pacman -Sc
```

## To completely remove all packages (Whether they are installed or uninstalled) from the cache:

```shell
sudo pacman -Scc
```

be careful using this command. There is no way to retrieve the cached packages once they are deleted.

## Mirrorlist

```shell
visudo /etc/pacman.d/mirrorlist
```

Generate a ranked mirror list with `reflector`
