# 1、Json基本用法

>`json.loads()`

把JSON格式字符串解码转成Python对象，从JSON到Python类型转换表如下：
|JSON   |	Python|
|---|---|
|object  |	dict|
|array	|list
|string	|str
|number(int)	|int
|number(real)|	float
|true	|True
|false|	False
|null|	None
>`json.dumps()`

Python类型的对象转换为json字符串


# 2、运用re、json、jsonpath包解析json思路
1. re：正则表达式，通过json的形式对症下药，写表达式去解析json；
```python
import re  
jsondata = {  
    "version": "23231cimesfedkk",  
    "result": {  
        "pages": 1314,  
        "data": [  
            {  
                "name": "大明",  
                "IDcard": "440588190001015688",  
                "address": "广东省广州市天河区正佳广场99楼520号",  
            },  
            {  
                "name": "二明",  
                "IDcard": "440588190012317456",  
                "address": "广东省广州市天河区天环广场88楼520号",  
            }  
        ]  
    }  
}  
  
if __name__ == '__main__':  
    name_list = re.findall(r"'name': '(\w*)'", str(jsondata))  
    IDcard_list = re.findall(r"'IDcard': '(\w*)'", str(jsondata))  # 身份证18位数字和字母组合  
    address_list = re.findall(r"'address': '(\w*)'", str(jsondata))  # 地址  
    print(name_list)  
    print(IDcard_list)  
    print(address_list)
```
2. json: 通过json中的json.loads()方法，将str类型转为dict类型，运用python字典的数据结构特点去解析json；
```python
# 若传入的数据为str类型需要将它转成dict类型  
# result = json.loads(jsondata)  
jsondata = jsondata["result"]["data"]  
resultdata = jsondata  
namelist=[]  
idcardlist=[]  
addresslist=[]  
for data in resultdata:  
    namelist.append(data['name'])  
    idcardlist.append(data['IDcard'])  
    addresslist.append(data['address'])  
print(namelist)  
print(idcardlist)  
print(addresslist)
```
3. jsonpath：对比与json包，jsonpath可以根据路径去解析json，比较适合用来解析json中带“[ ]”的数据。
## jsonpath学习

>jsonpath语法与Xpath的完整概述和比较

| Xpath | jsonpath | 概述                                   |
| :---- | :------- | :------------------------------------- |
| /     | $        | 根节点                                 |
| .     | @        | 当前节点                               |
| /     | .or[]    | 取子节点                               |
| *     | *        | 匹配所有节点                           |
| []    | []       | 迭代器标识（如数组下标，根据内容选值） |
| //    | ...      | 不管在任何位置，选取符合条件的节点     |
| n/a   | [,]      | 支持迭代器中多选                       |
| n/a   | ?()      | 支持过滤操作                           |
| n/a   | ()       | 支持表达式计算                         |
例子
```json
{ "store": {
    "book": [
      { "category": "reference",
        "author": "Nigel Rees",
        "title": "Sayings of the Century",
        "price": 8.95
      },
      { "category": "fiction",
        "author": "Evelyn Waugh",
        "title": "Sword of Honour",
        "price": 12.99
      },
      { "category": "fiction",
        "author": "Herman Melville",
        "title": "Moby Dick",
        "isbn": "0-553-21311-3",
        "price": 8.99
      },
      { "category": "fiction",
        "author": "J. R. R. Tolkien",
        "title": "The Lord of the Rings",
        "isbn": "0-395-19395-8",
        "price": 22.99
      }
    ],
    "bicycle": {
      "color": "red",
      "price": 19.95
    }
  }
}
```
### 获取符合条件的节点
想要过去author的值，如果采用【】一层一层的去剥取，就显得很麻烦，这时可以采用jsonpath
```python
import jsonpath
# $根节点 .取store节点 .取book节点 [*] 匹配所有book子节点 获取.author
author = jsonpath.jsonpath(data_json, '$.store.book[*].author')
print(author)


#或者  $..author 根节点下所有符合author的节点，如果有重复的名称节点，需要剥一层
author = jsonpath.jsonpath(data_json, '$..author') 
print(author)
```
### 使用指定索引
需要获取第三本书的价格
```python
third_book_price = jsonpath.jsonpath(data_json, '$.store.book[2].price')
print(third_book_price)
```
#### 获取含有isbn编号的书籍
```python
isbn_book = jsonpath.jsonpath(data_json, '$..book[?(@.isbn)]')
print(isbn_book)
print(type(isbn_book))
```
#### 将价格小于10元的书过滤出来
```python
book = jsonpath.jsonpath(data_json, '$..book[?(@.price<10)]')
print(book)
print(type(book))
```

[JSONPath在线验证https://www.jsonpath.cn](https://www.jsonpath.cn/)

https://goessner.net/articles/JsonPath/]