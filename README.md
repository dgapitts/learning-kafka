


# Getting started - setup on macosx

## Install kafka via brew


If you don´t have brew installed already


```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

next


```
brew install kafka
```


## Session one - first start zookeeper

```
cd /usr/local/opt/kafka        
./bin/zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties 
```

## Session two - next start kafka

```
/usr/local/opt/kafka/bin/kafka-server-start /usr/local/etc/kafka/server.properties
```


## Setup first topic

Note `bin/kafka-topics.sh` (as per the course instructions) is now `bin/kafka-topics``

```
/usr/local/opt/kafka $ bin/kafka-topics --create --topic mytopic --replication-factor 1 --partitions 1 --bootstrap-server localhost:9092
Created topic mytopic.
/usr/local/opt/kafka $ bin/kafka-topics --list --bootstrap-server localhost:9092
mytopic
/usr/local/opt/kafka $
```


## Setup first kafka-console-producer (session one)

```
/usr/local/opt/kafka $ bin/kafka-console-producer  --bootstrap-server localhost:9092 --topic mytopic
>hello
>kafka
>world
>1
>1
>2
>3
>5
>
>8
>13
>21
>
```


## Setup first kafka-console-consumer (session two)

```
~ $ cd /usr/local/opt/kafka
/usr/local/opt/kafka $ bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic mytopic --from-beginning
hello
kafka
world
1
1
2
3
5

8
13
21

```
