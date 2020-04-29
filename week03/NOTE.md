# 第三周 JavaScript中的特殊对象

## 原生对象
javaScript中的原生对象，提供了很多构造器，这些构造器一般都有一些私有字段。如：    
- Error: [[ErrorData]]
- Boolean: [[BooleanData]]
- Number: [[NumberData]]
- Date: [[DateValue]]
- RegExp: [[RegExpMatcher]]
- Symbol: [[SymbolData]]
- Map: [[MapData]]

## 函数对象与构造器对象
函数对象：具有[[call]]私有字段的对象  
构造器对象：具有[[construct]]私有字段的对象  
用户用function构造出来的对象同时具有[[call]]和[[construct]]字段，但他们的行为基本是一致的。  
而内置对象的构造器当作函数调用时，则产生不同的行为。


## 特殊行为的对象
- Array：Array 的 length 属性根据最大的下标自动发生变化
- Object.prototype：作为所有正常对象的默认原型，不能再给它设置原型了。
- String：为了支持下标运算，String 的正整数属性访问会去字符串里查找。
- Arguments：arguments 的非负整数型下标属性跟对应的变量联动。
- 模块的 namespace 对象：特殊的地方非常多，跟一般对象完全不一样，尽量只用于 import 吧。
- 类型数组和数组缓冲区：跟内存块相关联，下标运算比较特殊。
- bind 后的 function：跟原来的函数相关联。