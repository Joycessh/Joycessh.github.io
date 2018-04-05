
# JavaScript数据类型

## 六种数据类型(五种原始类型，一种对象类型)
- number
- sttring
- boolean
- null
- undefined
- object #对象
    - Function
    - Array
    - Date
    - ...

### javascript数据类型是弱数据类型，在定义变量时无需指定数据类型。

```
var num = 32;
num = "this is a string";

32 + 32  // 64 #加法运算
//"+"理解为字符串拼接，"-"理解为减法运算
"32" + 32 // "3232" # 字符串拼接
"32" - 32 // 0 # 减法运算
```

## 隐式转换

### 巧用“+”/"-"规则转换类型

```
var num = "string"；
num - 0 //将num对象转换为number

var num = 123；
num + "" //将num对象转换为string

```

### a === b #严格等于

- 首先判断类型，类型不同，返回false
- 类型相同：
  - number //数值一样
  - string //长度和内容都一样
  - null === null
  - undefined === undefined
  - NaN != NaN //NaN跟任何东西比较都不相等，包括跟自己比较。
  - new object != new object //就算是两个空对象，也不相等。
  - [1, 2] != [1, 2] //内容相同，顺序一样，也不相等，因为她们不是完全相同的对象
  - JavaScript中，对象的比较是用引用去比较的

### a == b #等于

- 类型相同，同===
- 类型不同，尝试类型转换再比较：
  - null == undefined //true
  - number == string //尝试把string转number，1 == "1.0"为true
  - boolean == ? //boolean转number，true = 1， false = 0
  - object == number | string //尝试把对象转为基本类型 new String('hh') == 'hi' //true
  - 其他：false

## 包装对象

```
var str = "string"; //string类型
var strObj = new String("string"); //对象类型，string对应的包装类
str.length //str为基本类型，没有属性。当str访问length属性时，javascript会把基本类型转换为对应的包装对象

```

## 类型检测

### typeof

{%note danger%}适合检测基本类型和function，遇到null失效{%endnote%}

```
typeof 100    "number"
typeof true     "boolean"
typeof function   "function"
typeof(undefined)  "undefined"
typeof new Object()   "object"
typeof [1, 2]           "object"
typeof NaN           "number"
typeof null         "object" #返回object而不是null，是由于历史原因

```

### instanceof

instanceof操作符是基于原型链去判断，用法：`obj instanceof Object`
注意： 不同的window或iframe之间的对象类型检测不能使用instanceof！

{%note danger%}可以用来检测自定义对象以及原生对象{%endnote%}

```
[1, 2] instanceof Array === true
new Object() instanceof Array ===false

```

### Object.prototype.toString.apply()

{%note%}适合内置对象和基本类型，用来检测null会存在兼容性问题{%endnote%}

```
Object.prototype.toString.apply([]); === "[object Array]"
Object.prototype.toString.apply(function(){}); === "[object Function]"
Object.prototype.toString.apply(null); === "[object Null]"
Object.prototype.toString.apply(unfefined); === "[object Undefined]"

IE6/7/8 Object.prototype.toString.apply(null); 返回"[object Object]"

```
