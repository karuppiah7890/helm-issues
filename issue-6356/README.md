```
$ helm install dummy issue-6356-chart/
$ helm upgrade dummy issue-6356-chart-new/
$ helm ls
$ helm upgrade dummy issue-6356-chart-new/
$ helm ls
$ helm upgrade dummy issue-6356-chart/
$ helm ls
```

releases information is stored in k8s secrets by default. there are other storages too, like configmaps and in-memory.
the above issue reproduction was done with secrets as release information storage.

have to check if the issue persists with other storage drivers (configmaps, in-memory) too and put a fix for it

looks like filtering is the problem, as all versions of the releases are listed when the storage is asked for releases information,
and then they are filtered based on some logic and then shown to the user

updated the complete issue information in the issue.