完整错误信息：

java.lang.ClassCastException: [Ljava.lang.String; cannot be cast to java.lang.String

 报这个错的原因是：

将  [Ljava.lang.String; 代表的数组类型强制转换为 java.lang.String 代表的字符串类型两者类型不匹配导致出错

注:[Ljava.lang.String@1b634e7  -- 
   "[" 表示一维数组 
    "[["表示二维数组 
    "L"表示一个对象 
    "java.lang.String"表示对象的类型 
    "@"后面表示该对象的HashCode