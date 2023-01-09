```java
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'bondSentimentNewsEssenceServiceImpl': Injection of resource dependencies failed; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'esBondSentimentNewsEssenceDAO': Injection of resource dependencies failed; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'sentimentNewsEssenceRepository': Post-processing of FactoryBean's singleton object failed; nested exception is java.lang.IllegalStateException: Failed to introspect Class [com.github.wz2cool.elasticsearch.repository.support.SimpleElasticsearchExtRepository] from ClassLoader [sun.misc.Launcher$AppClassLoader@18b4aac2]  
   at org.springframework.context.annotation.CommonAnnotationBeanPostProcessor.postProcessProperties(CommonAnnotationBeanPostProcessor.java:337)   at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1422)   at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:594)
```

Failed to introspect Class [com.github.wz2cool.elasticsearch.repository.support.SimpleElasticsearchExtRepository] from ClassLoader

调整maven版本和包内版本