---
title: Swap
date-modified: 2023-07-24
---

## Check swappiness

```
cat /proc/sys/vm/swappiness
```

Default is `60`. Accepted  value is in range of 0-100.\
Low value - little swapping, high value - aggressive swapping.

## Change swappiness

Run as root:
```
sysctl vm.swappiness=x
```

Where `x` is number in range of 0 - 100.

## Clear swap

Did you try to turn it off an on again?

Clear swap by turning it off. This will move swap content to RAM.

1. Check that you have enough RAM to fit swap:
    ```
    free -mh
    ```
    Mem free should be larger than Swap total.

2. Turn off swap, as root:
    ```
    swapoff -a
    ```

3. Turn on swap, as root:
    ```
    swapon -a
    ```

4. Enjoy life

