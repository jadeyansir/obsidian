```java
18:19:13.502 [Thread-2] ERROR TopicListener[process:128] - process error! ThreadID: 16

org.springframework.dao.DataIntegrityViolationException: PreparedStatementCallback; SQL [insert into estate_bond_finance("REFERENCE_YIELD", "CREATE_TIME", "COM_FULL_NAME", "COM_SHORT_NAME", "BOND_SHORT_NAME", "COM_UNI_CODE", "BOND_UNI_CODE", "VALID", "CREATE_BY", "UPDATE_TIME", "BOND_FULL_NAME", "LISTING_STATUS", "BOND_CODE", "ISSUE_COUPON_RATE", "REMAINING_TENOR", "BOND_ISSUE_BALANCE", "ID", "INTERNATIONAL", "UPDATE_BY", "LISTING_DATE") values (?, to_date(?, 'yyyy-mm-dd hh24:mi:ss'), ?, ?, ?, ?, ?, ?, ?, to_date(?, 'yyyy-mm-dd hh24:mi:ss'), ?, ?, ?, ?, ?, ?, ?, ?, ?, to_date(?, 'yyyy-mm-dd'))]; ORA-02290: check constraint (DM.SYS_C0013971) violated

; nested exception is java.sql.SQLIntegrityConstraintViolationException: ORA-02290: check constraint (DM.SYS_C0013971) violated



	at org.springframework.jdbc.support.SQLExceptionSubclassTranslator.doTranslate(SQLExceptionSubclassTranslator.java:85)

	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:73)

	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:82)

	at org.springframework.jdbc.core.JdbcTemplate.execute(JdbcTemplate.java:649)

	at org.springframework.jdbc.core.JdbcTemplate.update(JdbcTemplate.java:870)

	at org.springframework.jdbc.core.JdbcTemplate.update(JdbcTemplate.java:931)

	at org.springframework.jdbc.core.JdbcTemplate.update(JdbcTemplate.java:941)

	at com.innodealing.dmsyncclient.service.DatabaseService.replaySql(DatabaseService.java:42)

	at com.innodealing.dmsyncclient.service.DatabaseService$$FastClassBySpringCGLIB$$ff54764d.invoke(<generated>)

	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:204)

	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:738)

	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:157)

	at org.springframework.transaction.interceptor.TransactionInterceptor$1.proceedWithInvocation(TransactionInterceptor.java:99)

	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:282)

	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)

	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)

	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:673)

	at com.innodealing.dmsyncclient.service.DatabaseService$$EnhancerBySpringCGLIB$$bebf4f7d.replaySql(<generated>)

	at com.innodealing.dmsyncclient.service.SyncService.relaySql(SyncService.java:184)

	at com.innodealing.dmsyncclient.service.SyncService.processMessage(SyncService.java:173)

	at com.innodealing.dmsyncclient.listener.TopicListener.handleMessage(TopicListener.java:143)

	at com.innodealing.dmsyncclient.listener.TopicListener.process(TopicListener.java:123)

	at java.lang.Thread.run(Thread.java:748)

Caused by: java.sql.SQLIntegrityConstraintViolationException: ORA-02290: check constraint (DM.SYS_C0013971) violated
```
Oracle初始建表语句
```java
CREATE TABLE "DM"."ESTATE_BOND_FINANCE" 
   (	"ID" NUMBER(19,0) NOT NULL ENABLE, 
	"COM_UNI_CODE" NUMBER(19,0) DEFAULT NULL, 
	"COM_FULL_NAME" VARCHAR2(200) DEFAULT NULL, 
	"COM_SHORT_NAME" VARCHAR2(100) DEFAULT NULL, 
	"BOND_UNI_CODE" NUMBER(19,0) DEFAULT NULL, 
	"BOND_FULL_NAME" VARCHAR2(200) DEFAULT NULL, 
	"BOND_SHORT_NAME" VARCHAR2(100) DEFAULT NULL, 
	"BOND_CODE" VARCHAR2(50) DEFAULT NULL, 
	"ISSUE_COUPON_RATE" NUMBER(8,4) DEFAULT NULL, 
	"REFERENCE_YIELD" NUMBER(8,4) DEFAULT NULL, 
	"BOND_ISSUE_BALANCE" NUMBER(8,4) DEFAULT NULL, 
	"REMAINING_TENOR" VARCHAR2(50) DEFAULT NULL, 
	"LISTING_DATE" DATE DEFAULT NULL, 
	"LISTING_STATUS" NUMBER(3,0) DEFAULT NULL, 
	"INTERNATIONAL" NUMBER(3,0) DEFAULT NULL, 
	"VALID" NUMBER(3,0) DEFAULT NULL, 
	"CREATE_BY" NUMBER(19,0) DEFAULT NULL, 
	"CREATE_TIME" TIMESTAMP (0) DEFAULT SYSTIMESTAMP, 
	"UPDATE_BY" NUMBER(19,0) DEFAULT NULL, 
	"UPDATE_TIME" TIMESTAMP (0) DEFAULT SYSTIMESTAMP, 
	 CHECK (id > 0) ENABLE, 
	 CHECK (com_uni_code > 0) ENABLE, 
	 CHECK (bond_uni_code > 0) ENABLE, 
	 CHECK (listing_status > 0) ENABLE, 
	 CHECK (international > 0) ENABLE, 
	 CHECK (create_by > 0) ENABLE, 
	 CHECK (update_by > 0) ENABLE, 
	 PRIMARY KEY ("ID")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "DM_DATA"  ENABLE, 
	 CONSTRAINT "SYS_C0013982" CHECK (valid >= 0) ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 
 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "DM_DATA"
```
可以看到多个字段数值存在必须大于0的，，，如果一旦数据有=0的就会报错