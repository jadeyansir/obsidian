> Date类型数据转换异常

## 解决方法
序列化时进行格式化转换`@JsonFormat(pattern = "yyyy-MM-dd")`
```java
@ExcelProperty("统计日期")  
@ColumnWidth(50)  
@JsonFormat(pattern = "yyyy-MM-dd")  
private Date statDate;
```