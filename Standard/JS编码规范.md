#1. 变量命名规范

变量名包括全局变量，局部变量，类变量，函数参数等等，他们都属于这一类。

##基本规范

变量命名都以类型前缀+有意义的单词组成，单词首字母都需要大写。例如：sUserName，nCount。

##前缀规范

每个局部变量都需要有一个类型前缀，按照类型可以分为：

s：表示字符串。例如：```sName```，```sHtml```；

n：表示数字。例如：```nPage```，```nTotal```；

b：表示逻辑。例如：```bChecked```，```bHasLogin```；

a：表示数组。例如：```aList```，```aGroup```；

r：表示正则表达式。例如：```rDomain```，```rEmail```；

f：表示函数。例如：```fGetHtml```，```fInit```；

o：表示以上未涉及到的其他对象，例如：```oButton```，```oDate```；

例外情况：

1：作用域不大临时变量可以简写，比如：```str，num，bol，obj，fun，arr```。

2：循环变量可以简写，比如：```i，j，k```等。

为什么需要这样强制定义变量前缀？正式因为javascript是弱语言造成的。在定义大量变量的时候，我们需要很明确的知道当前变量是什么属性，如果只通过普通单词，是很难区分的。

全局变量以及常量规范

研发中心，前端是基于“类”的概念来来开发javascript的（稍后会专门介绍），每个类定义都是在一个闭包函数中，除了在window下有类的定义而外，只允许有两种变量定义在全局，那就是全局变量和常量。

全局变量使用g作为前缀，定义在window下。例如 ```gUserName，gLoginTime``` 。

某些作为不允许修改值的变量认为是常量，全部字母都大写。例如：```COPYRIGHT，PI```。常量可以存在于函数中，也可以存在于全局。

#2. 函数命名规范

统一使用动词或者动词[＋名词]形式，例如：fGetVersion()，fSubmitForm()，fInit()；涉及返回逻辑值的函数可以使用```is，has```等表示逻辑的词语代替动词。

如果有内部函数，使用```_f+动词[+名词]```形式，内部函数必需在函数最后定义。

对象方法实现

对象方法命名使用 ```f+对象类名+动词[+名词]```形式；例如 ```fAddressGetEmail```

事件响应函数

某事件响应函数命名方式为触发事件对象名＋事件名或者模块名＋触发事件对象名＋事件名，例如：```fDivClick()，fAddressSubmitButtonClick()```

#3.其他注意事项

1.所有命名最好使用英语表示。

2.所有变量名应该明确而必要，尽量避免不必要的容易混淆的缩写。

3.netease.events.mouse.Handler，而不是 ```netease.events.mouse.MouseEventHandler```。

4.对应的方法应该使用对应的动词，例如：```get/set, add/remove, create/destroy, start/stop, insert/delete, begin/end```。

5.应该避免双重否定意义的变量，例如：```bIsNotError bIsNotFound```，不可取。

6.变量应该在最小的范围内定义，并尽可能的保持最少的活动时间。

7.循环变量最好在循环中定义。例如：


```javascript
	for(var i=0,m=10;i<m;i++){
		do something
	} 
```

8.尽量避免复杂的条件语句，可以使用临时的```boolean```变量代替。

9.一定要避免在条件中执行语句，例如：
 
```javascript
	if((i=3)>2){} 
```
以上办法不可取。

10.不要在代码中重复使用相同意义的数字，用一个变量代替，比如 ```nTotal=100; num= total``` 。

邮箱事业部页面在window只允许定义三种变量——1：全局变量；2：常量；3：类。任何业务逻辑都需要通过类方法或者示例方法实现。前两种变量在之前文章中已经介绍，在此不再累述，接下来详细介绍类定义和使用的规范。

##这里需要特别说明以下几点：

1.方法的定义不是通过匿名函数来定义，而是集中在类定义的下面来实现。这样的好处是能在最开始将类的属性方法定义都罗列出来，便于通过源码查看到对应属性和方法。

2.在类/实例方法中，使用局部变量代替this。this不是一个好的玩意儿，一不小心就会被this搞晕。使用局部变量能够尽量避免这样的问题，也能够在压缩混淆的时候效果更好。

3.在实际开发过程中，每个类定义都单独一个js实现。

除了类的定义，闭包不实现 任何其他逻辑。使用闭包能够将很多变量约束在闭包作用域中，并且能够在压缩混淆中效果更好，除此之外，使用闭包定义类，在之后将介绍到的动态加载成为了一件十分容易的事情，稍后会和大家一起分享。
