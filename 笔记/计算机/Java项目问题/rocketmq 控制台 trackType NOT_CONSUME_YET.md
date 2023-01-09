消息消费异常，原因大概有下面几种
1.  producer发送失败
2.  consumer消费异常
3.  consumer根本就没收到消息

**消息没找到**

说明proder发送异常，也有可能是消息过期了，因为rocketmq的消息默认保存72h，此时到producer端的日志进一步确认即可

**消息找到了**
接着看消息的消费状态，比如消费状态为NOT_ONLINE

```java
public enum TrackType {  
    CONSUMED,  
    CONSUMED_BUT_FILTERED,  
    PULL,  
    NOT_CONSUME_YET,  
    NOT_ONLINE,  
    UNKNOWN  
}
```
上面是所有状态类型，每种类型的解释如下

| 类型                  | 解释                   |
| :-------------------- | :--------------------- |
| CONSUMED              | 消息已经被消费         |
| CONSUMED_BUT_FILTERED | 消息已经投递但被过滤   |
| PULL                  | 消息消费的方式是拉模式 |
| NOT_CONSUME_YET       | 目前没有被消费         |
| NOT_ONLINE            | CONSUMER不在线         |
| UNKNOWN               | 未知错误               |

针对标题的问题
mq控制台 显示有该条消息数据 只是状态为未消费 那么问题应该出在消费者一方
排查代码后发现
>消费者consumeMessage方法里出现空指针的代码，这样造成了该条消息没有返回ConsumeOrderlyStatus状态 标记为已消费，所以一直循环消费该消息 日志里循环打印