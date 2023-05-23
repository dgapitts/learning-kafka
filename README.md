


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

