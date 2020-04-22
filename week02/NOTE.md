# 第二周
## 编程语言通识
### 形式语言与非形式语言
1. 非形式语言：人类语言(英语、汉语等)
2. 形式语言：乔姆斯基谱系

 2.1 0型 无限制文法 <a><b> ::= <c><d> 

 	等号左边可以有多个生成项  

 	javaScript中的get就属于无限制文法

 2.2 1型 上下文相关文法 "a" <b> "c" ::= "a" "x" "c" 

 	上下文"a"和"c"不变，中间的b可以变

 2.3 2型 上下文无关文法 <a> ::= "xxx" 

 2.4 3型 正则 <a> ::= <a>? 

 	只允许左递归  
 	javaScript表达式在 ** 出现之前是3型的，出现之后就成了2型的

从0型到3型，限制和严格性逐渐增强。  大多数编程语言都是2型文法为主体的，偶尔会出现某些特例。  
对于编译器而言，限制越严格，越容易实现。
文法分为词法和语法。词法分析：用正则扫一遍，把各个单词拆出来

### BNF产生式
举个栗子：规定一门语言，只能由"a"和"b"两种语言构成，可以这样写：
```javascript
<Programm>= <Programm> "a"+ | <Programm> "b"+
````

再举个栗子，定义一个四则运算  
先定义十进制的数字：  
```javascript
<Number> = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
<DecimalNumber> = "0" | (("1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9") <Number>*)
````
然后定义加法和乘法运算：
```javascript
<MultiplicativeExpression> = <DecimalNumber> | 
	<MultiplicativeExpression> "*" <DecimalNumber> |
	<MultiplicativeExpression> "/" <DecimalNumber>

<AdditiveExpression> = <MultiplicativeExpression> | 
	<MultiplicativeExpression> "+" <DecimalNumber> |
	<MultiplicativeExpression> "-" <DecimalNumber>
````

逻辑运算：
```javascript
<LogicalExpression> = <AdditiveExpression> |
	<LogicalExpression> "||" <AdditiveExpression> |
	<LogicalExpression> "&&" <AdditiveExpression>

````

以及带括号的四则运算：
```javascript
<PrimaryExpression> = <DecimalNumber> |
	"(" <LogicalExpression> ")"
````
### 图灵完备
计算机语言必须是图灵完备的，一般通过两种方式实现：
1. goto/ if while
2. lambda递归

### 动态和静态
动态和静态语言的显著区别在于类型系统  
强弱类型语言的区分在于有无隐式类型转换  
动态不等于强类型 静态不等于弱类型

### 编程语言的粒度划分
Atom-Expression-Statement-Structure-Program

##  javaScript词法及类型
### Unicode
最早的字符集：ASCII，所有字符集都支持ASCII，兼容性最好  
四位16进制unicode范围内的字符称为BMP，js中charCode系列API只能处理BMP范围内的字符，超出该范围需要用fromCodePoint和codePointAt系列  
javaScript的最佳实践是将输入限定在ASCII范围内，或者BMP内，如果超出该范围建议用\u转义，如：
```javascript
var \u5389\u5bb3 = 1;
````
### InputElement
#### WhiteSpace
TAB制表符  
VT垂直制表符  
FF
SP
NBSP
ZWNBSP

#### Terminator
LF
CR
...
#### Comment
#### Token
1. Punctuator  
2. Keywords  
3. Identifier
变量名：不能用keywords；属性名可以用   
4. Literal
- Number
	0b 二进制
	0o 八进制
	0x 十六进制
parseInt(09)在浏览器中的运行结果可能不是9，因为有时0开头的数会被解析为八进制，可以用parseInt(09, 10)  

比较浮点数最佳实践：
```javascript
Math.abs(0.1 + 0.2 - 0.3) < Number.EPSILON
````

97.toString(2)为什么会报错？因为会当成小数点解析  
97 .toString(2)是合法输入

- String
USC即BMP范围
UTF-8不一定比UTF-16更省内存，因为UTF-8会使用三段式存储
- Bollean
- Null
- Undefined
