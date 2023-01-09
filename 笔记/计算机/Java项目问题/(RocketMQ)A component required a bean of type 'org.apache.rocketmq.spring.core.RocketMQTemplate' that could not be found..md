```java
Description:  
  
A component required a bean of type 'org.apache.rocketmq.spring.core.RocketMQTemplate' that could not be found.  
  
The following candidates were found but could not be injected:  
   - Bean method 'rocketMQTemplate' in 'RocketMQAutoConfiguration' not loaded because AnyNestedCondition 0 matched 2 did not; NestedCondition on RocketMQAutoConfiguration.ProducerOrConsumerPropertyCondition.DefaultLitePullConsumerExistsCondition @ConditionalOnBean (types: org.apache.rocketmq.client.consumer.DefaultLitePullConsumer; SearchStrategy: all) did not find any beans of type org.apache.rocketmq.client.consumer.DefaultLitePullConsumer; NestedCondition on RocketMQAutoConfiguration.ProducerOrConsumerPropertyCondition.DefaultMQProducerExistsCondition @ConditionalOnBean (types: org.apache.rocketmq.client.producer.DefaultMQProducer; SearchStrategy: all) did not find any beans of type org.apache.rocketmq.client.producer.DefaultMQProducer  
  
  
Action:  
  
Consider revisiting the entries above or defining a bean of type 'org.apache.rocketmq.spring.core.RocketMQTemplate' in your configuration.
```
**配置文件里没有加 producer.group**
原先是
```java
# rocket mq  
rocketmq.name-server=192.168.8.49:9876  
rocketmq.producer.access-key=superadmin  
rocketmq.producer.secret-key=12345678  
```
需要加一个
```java
# rocket mq  
rocketmq.name-server=192.168.8.49:9876  
rocketmq.producer.access-key=superadmin  
rocketmq.producer.secret-key=12345678
rocketmq.producer.group=international-sentiment-service-producer
```
