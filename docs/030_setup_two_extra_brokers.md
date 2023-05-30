### Starting two extra brokers 



```
/usr/local/opt/kafka $ diff ./.bottle/etc/kafka/server.properties ./.bottle/etc/kafka/server-1.properties
24c24
< broker.id=0
---
> broker.id=1
34c34
< #listeners=PLAINTEXT://:9092
---
> listeners=PLAINTEXT://:9093
62c62
< log.dirs=/usr/local/var/lib/kafka-logs
---
> log.dirs=/usr/local/var/lib/kafka-logs-1
/usr/local/opt/kafka $ diff ./.bottle/etc/kafka/server-1.properties ./.bottle/etc/kafka/server-2.properties
24c24
< broker.id=1
---
> broker.id=2
34c34
< listeners=PLAINTEXT://:9093
---
> listeners=PLAINTEXT://:9094
62c62
< log.dirs=/usr/local/var/lib/kafka-logs-1
---
> log.dirs=/usr/local/var/lib/kafka-logs-2
```


Start broker.id=1 in one session

```
/usr/local/opt/kafka $ ./bin/kafka-server-start ./.bottle/etc/kafka/server-1.properties
...
```

Start broker.id=2 in another session
```
/usr/local/opt/kafka $ ./bin/kafka-server-start ./.bottle/etc/kafka/server-2.properties
...
```
