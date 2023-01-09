**特别注意**：Oracle<font color="#ff0000">不允许</font>修改字段精度或者长度，所以就会有下面的问题。

### 数据传输时
如果通过canal进行数据表的同步时，DDL语句会直接报错，这样就会造成canal数据出现严重<font color="#ff0000">堵塞</font>。
	解决方法：
	每次进行DDL语句操作时，必须将canal中该条语句跳过去，进行下面的DML语句

### 修改方法
1. 将要修改的字段重命名为其他名称
2. 创建修改精度后的字段
3. 复制重命名字段数据到修改后精度字段
4. 删除重命名字段
全部SQL如下
```sql
ALTER TABLE estate_bond_finance RENAME COLUMN  reference_yield TO reference_yield_temp;
ALTER TABLE estate_bond_finance ADD reference_yield NUMBER(18, 4);
UPDATE estate_bond_finance SET reference_yield=reference_yield_temp;
ALTER TABLE estate_bond_finance DROP COLUMN reference_yield_temp;
```
