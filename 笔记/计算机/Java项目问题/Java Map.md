Map.compute
```java
sentimentIdTOAreaNameStrMap.compute(sentimentRelaAreaDO.getSentimentId(), (k, v) -> {  
    if (sentimentIdTOAreaNameStrMap.containsKey(k)) {  
        v.add(areaNameStr);  
        return v;  
    }  
    return Lists.newArrayList(areaNameStr);  
});
```
Map.computeIfPresent
```java
sentimentIdTOAreaNameStrMap.computeIfPresent(sentimentRelaAreaDO.getSentimentId(), (k, v) -> {  
    if (sentimentIdTOAreaNameStrMap.containsKey(k)) {  
        v.add(areaNameStr);  
        return v;  
    }  
    return Lists.newArrayList(areaNameStr);  
});
```
区别
computeIfPresent，不在map里面的数据不会放进去；compute会放进去

compute适合一个空map重新一个一个赋值
computeIfPresent适合对map进行修改的操作