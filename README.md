The traffic docker container is located at https://quay.io/repository/splunko11ytest/network-explorer-debug/traffic.

To deploy:
```
helm install traffic-server traffic-server/ --values traffic-server/values.yaml
helm install traffic-client traffic-client/ --values traffic-client/values.yaml
```

```
k get pods | rg traffic
traffic-client-77d8fc5997-t8pct                           1/1     Running   0               89s
traffic-server-d5f445576-9scn9                            1/1     Running   0               3m30s
```

```
k logs -f traffic-server-d5f445576-9scn9
<snip>
[2022-12-14 02:53:03.388] [info] server_monitor: port 1139; new(10)/cmltv(1531) connects; actv 88 ms ago
[2022-12-14 02:53:04.388] [info] server_monitor: port 1139; new(10)/cmltv(1541) connects; actv 86 ms ago
[2022-12-14 02:53:05.388] [info] server_monitor: port 1139; new(10)/cmltv(1551) connects; actv 75 ms ago
[2022-12-14 02:53:06.388] [info] server_monitor: port 1139; new(10)/cmltv(1561) connects; actv 75 ms ago
<snip>
```


```
k logs -f traffic-client-77d8fc5997-t8pct
<snip>
[2022-12-14 02:53:04.006] [info] timed_client(1): to traffic-server:1139 sent #1538/100000000
[2022-12-14 02:53:04.102] [info] timed_client(1): to traffic-server:1139 sent #1539/100000000
[2022-12-14 02:53:04.202] [info] timed_client(1): to traffic-server:1139 sent #1540/100000000
[2022-12-14 02:53:04.302] [info] timed_client(1): to traffic-server:1139 sent #1541/100000000
<snip>
```

