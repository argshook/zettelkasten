---
title: pacman
date-modified: 2024-09-03
---

## Checking Cache

```shell
# Count cached packages
sudo ls /var/cache/pacman/pkg/ | wc -l

# Check disk space used
du -sh /var/cache/pacman/pkg/
```

## Cleaning Cache

```shell
# Remove all but 3 most recent versions
sudo paccache -r

# Keep only 1 most recent version
sudo paccache -rk 1

# Remove all cached versions of uninstalled packages
sudo paccache -ruk0

# Remove all uninstalled packages
sudo pacman -Sc

# Remove all packages from cache (use with caution)
sudo pacman -Scc
```

## Mirrorlist Management

```shell
# Edit mirrorlist
visudo /etc/pacman.d/mirrorlist

# Generate ranked mirror list
reflector [options]
```

Note: Always verify changes before applying. Backup important files.
