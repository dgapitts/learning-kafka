### kafka-configs and changing unclean.leader.election

Firstly some notes on [unclean leader election](https://medium.com/lydtech-consulting/kafka-unclean-leader-election-13ac8018f176)
> The unclean leader election configuration is used to determine whether a replica that is not in-sync with the lead replica can itself become leader in a failure scenario. However if this were to happen, any messages that the unclean leader did not have would be lost.


Next reviewing all settings
```
/usr/local/opt/kafka $ kafka-configs --bootstrap-server localhost:9092 --entity-type topics --entity-name mytopic --describe --all
All configs for topic mytopic are:
  compression.type=producer sensitive=false synonyms={DEFAULT_CONFIG:compression.type=producer}
  leader.replication.throttled.replicas= sensitive=false synonyms={}
  message.downconversion.enable=true sensitive=false synonyms={DEFAULT_CONFIG:log.message.downconversion.enable=true}
  min.insync.replicas=1 sensitive=false synonyms={DEFAULT_CONFIG:min.insync.replicas=1}
  segment.jitter.ms=0 sensitive=false synonyms={}
  cleanup.policy=delete sensitive=false synonyms={DEFAULT_CONFIG:log.cleanup.policy=delete}
  flush.ms=9223372036854775807 sensitive=false synonyms={}
  follower.replication.throttled.replicas= sensitive=false synonyms={}
  segment.bytes=1073741824 sensitive=false synonyms={DEFAULT_CONFIG:log.segment.bytes=1073741824}
  retention.ms=259200000 sensitive=false synonyms={DYNAMIC_DEFAULT_BROKER_CONFIG:log.retention.ms=259200000, STATIC_BROKER_CONFIG:log.retention.hours=168, DEFAULT_CONFIG:log.retention.hours=168}
  flush.messages=9223372036854775807 sensitive=false synonyms={DEFAULT_CONFIG:log.flush.interval.messages=9223372036854775807}
  message.format.version=3.0-IV1 sensitive=false synonyms={DEFAULT_CONFIG:log.message.format.version=3.0-IV1}
  max.compaction.lag.ms=9223372036854775807 sensitive=false synonyms={DEFAULT_CONFIG:log.cleaner.max.compaction.lag.ms=9223372036854775807}
  file.delete.delay.ms=60000 sensitive=false synonyms={DEFAULT_CONFIG:log.segment.delete.delay.ms=60000}
  max.message.bytes=1048588 sensitive=false synonyms={DEFAULT_CONFIG:message.max.bytes=1048588}
  min.compaction.lag.ms=0 sensitive=false synonyms={DEFAULT_CONFIG:log.cleaner.min.compaction.lag.ms=0}
  message.timestamp.type=CreateTime sensitive=false synonyms={DEFAULT_CONFIG:log.message.timestamp.type=CreateTime}
  preallocate=false sensitive=false synonyms={DEFAULT_CONFIG:log.preallocate=false}
  min.cleanable.dirty.ratio=0.5 sensitive=false synonyms={DEFAULT_CONFIG:log.cleaner.min.cleanable.ratio=0.5}
  index.interval.bytes=4096 sensitive=false synonyms={DEFAULT_CONFIG:log.index.interval.bytes=4096}
  unclean.leader.election.enable=false sensitive=false synonyms={DEFAULT_CONFIG:unclean.leader.election.enable=false}
  retention.bytes=-1 sensitive=false synonyms={DEFAULT_CONFIG:log.retention.bytes=-1}
  delete.retention.ms=86400000 sensitive=false synonyms={DEFAULT_CONFIG:log.cleaner.delete.retention.ms=86400000}
  segment.ms=604800000 sensitive=false synonyms={}
  message.timestamp.difference.max.ms=9223372036854775807 sensitive=false synonyms={DEFAULT_CONFIG:log.message.timestamp.difference.max.ms=9223372036854775807}
  segment.index.bytes=10485760 sensitive=false synonyms={DEFAULT_CONFIG:log.index.size.max.bytes=10485760}
```

Now reviewing unclean.leader.election.enable


```
/usr/local/opt/kafka $ kafka-configs --bootstrap-server localhost:9092 --entity-type topics --entity-name mytopic --describe --all|grep leader

  leader.replication.throttled.replicas= sensitive=false synonyms={}
  unclean.leader.election.enable=false sensitive=false synonyms={DEFAULT_CONFIG:unclean.leader.election.enable=false}
```

Then change unclean.leader.election.enable 


```
/usr/local/opt/kafka $
/usr/local/opt/kafka $ kafka-configs --bootstrap-server localhost:9092 --entity-type topics --entity-name mytopic --alter --add-config unclean.leader.election.enable=true
Completed updating config for topic mytopic.
```

Finally reviewing unclean.leader.election.enable

```
/usr/local/opt/kafka $ kafka-configs --bootstrap-server localhost:9092 --entity-type topics --entity-name mytopic --describe --all|grep leader
  leader.replication.throttled.replicas= sensitive=false synonyms={}
  unclean.leader.election.enable=true sensitive=false synonyms={DYNAMIC_TOPIC_CONFIG:unclean.leader.election.enable=true, DEFAULT_CONFIG:unclean.leader.election.enable=false}
```
