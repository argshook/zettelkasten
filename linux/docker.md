---
title: Docker
date-modified: 2022-07-12
---

Remove all docker containers and images.
For when you need a cleanup

```shell
docker rm $(docker ps -aq) && docker rmi $(docker images -q)
```

