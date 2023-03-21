# golang基础

## Go语言设计哲学

> 追求简单，少即是多

+ 简洁，常规语法（不需要解析符号表）
+ 内置垃圾收集，降低内存管理的心智负担
+ 没有头文件
+ 显式依赖(package)
+ 没有循环依赖(package)
+ 常量只是数字
+ 首字母大小写决定可见性
+ 没有子类型继承（没有子类）
+ 没有算术转换
+ 接口是隐式的（不需要implements声明）
+ 方法就是函数
+ 接口只是方法结合（没有数据）
+ 方法仅按名称匹配（不是按类型）
+ 没有构造函数和析构函数
+ n++和n--是语句，而不是表达式
+ 没有++n和--n
+ 赋值不是表达式
+ 在赋值和函数调用中定义的求值顺序（没有”序列点“概念）
+ 没有指针算术
+ 内存总是初始化为零值
+ 没有类型注解语法（比如 static public）
+ 没有异常（exception）
+ 内置字符串、切片、map类型
+ 内置数组边界检查
+ 内置并发支持

> 偏好组合，正交解耦

主流语言通过自上而下的类型体系、继承、显示接口将程序各部分耦合，go通过 **组合** 将各部分耦合。

Go正交语法:
+ Go无类型体系，类型之间是独立的，没有子类型
+ 每个类型都可以有自己的方法集合，类型定义和方法实现是正交独立的
+ 接口与其实现之间隐式关联
+ 包之间是相对独立的，没有子包的概念

Go组合方式
+ 类型嵌入（类似继承机制，但是原理上与其完全不同）
+ 被嵌入的类型和新类型之间没有任何关系（类型嵌入**垂直组合**）
+ 接口将程序各个部分组合起来（接口嵌入**水平组合**）
+ go + channel 的组合

总结，组合的应用塑造了Go程序的骨架接口。类型嵌入为类型提供垂直扩展的能力，接口是水平组合

> 原生并发，轻量高效（并发是有关结构的，而并行是有关执行的）

+ 采用轻量级协程并发模型
+ 并发的语法元素和机制
+ 并发原则

> 面向工程，”自带电池“

工程主要遇到的问题
+ 程序构建慢
+ 失控的依赖管理
+ 开发人员使用的编程语言的不同子集 （写法不一样）
+ 代码可理解性差（代码可读性差、文档差等）
+ 功能重复实现
+ 升级更新消耗大
+ 实现自动化工具难度高
+ 版本问题
+ 跨语言构建问题

## go语言特性

+ 内置并发编程支持
	+ 使用协程（groutine）作为基本的计算单元。轻松的创建协程
	+ 使用通道（channel）来实现协程间的同步和通信
+ 内置映射（map）和切片（slice）类型
+ 支持多态
+ 使用接口（interface）来实现装盒（value boxing）和反射（reflection）
+ 支持指针
+ 支持函数闭包（closure）
+ 支持方法
+ 支持延迟函数调用（defer）
+ 支持类型内嵌
+ 支持类型推断
+ 内存安全
+ 自动垃圾回收
+ 良好的代码跨平台
+ 自定义泛型

## go语言原生编程思维

> 组合，并发


## 关键字
> go关键字25个

|关键字|含义|
|-|-|
|**>声明<**|**6个**|
|const|常量|
|func|函数|
|import|包导入|
|package|包|
|type|类型定义|
|var|声明|
|**>组合类型的表示<**|**4个**|
|chan|通道|
|interface|接口|
|map|映射|
|struct|结构体|
|**>流程控制<**|**13个**|
|break|打断|
|case|分支|
|continue|继续|
|default|默认|
|else|另外的|
|fallthrough|穿透|
|for|循环|
|goto|转到|
|if|判断|
|range|区间|
|return|返回|
|select|选择，挑选|
|switch|切换|
|**>协程和延迟函数调用<**|**2个**|
|defer|延迟|
|go|协程|

### 关键字和标识符中涉及的名词解释
+ 关键字：是一些特殊的用来帮助编译器理解和解析源代码的单词
+ 标识符：是以Unicode字母或者_开头并且完全由Unicode字符和Unicode数字组成的单词
+ 标识符 _ 是一个特殊字符，它叫空标识符
+ 大写开头的标识符称为**导出标识符**（公开）
+ 小写的是**非导出**（私有）
+ 中文字符被视为非导出字符

## 内置类型

|名称|含义|
|-|-|
|**>值类型<**||
|bool|布尔|
|int(32或64)|有符号|
|int8|8位|
|int16|16位|
|int32|32位|
|int64|64位|
|uint(32或64)|无符号|
|uint8别名byte|8位|
|uint16|16位|
|uint32|32位|
|uint64|64位|
|float32|浮点32位|
|float64|浮点64位|
|array|数组|
|**>引用类型<**||
|slice|切片|
|map|映射|
|chan|通道|

### 基本类型和字面量涉及的名词解释
+ 类型（type）可以看做值（value）的模板，值可以看做类型的实例
+ 内置类型也称为预声明类型
+ 任意类型的所有值的尺寸都是相同的，所以一个值的尺寸也常称为它的类型的尺寸
+ 字面量：一个值的字面形式称为一个字面量，它表示此值在代码中文字体现

## 常量和变量

## 内置函数
> 有一些一般用不到的函数就不记录了

|名称|含义|
|-|-|
|append|数组，切片，追加元素|
|close|关闭通道|
|delete|删除映射中key和对应的value|
|panic|异常|
|recover|恢复异常|
|make|分配内存 切片，映射，通道|
|new|分配内存，主要是Type类型的指针|
|cap|容量，切片和映射|
|copy|用于复制和连接切片|
|len|长度，字符串，数组，切片，映射，通道|
|print,println|打印，一般还是使用fmt包|


## 尽量定义零值可用的类型
> 零值不仅在变量初始化阶段避免了变量值不确定可能带来的潜在问题，定义零值可用类型是**最佳实践之一**

go语言每个原生类型都有默认值，这就是类型的零值

+ 所有整数类型：0
+ 浮点类型：0.0
+ 布尔类型：false
+ 字符串类型：""
+ 指针、interface、切片、channel、map、function：nil

> 零值可用
保持与Go一致的理念，给自定义的类型一个合理的零值，并尽量保持自定义类型的零值可用

## 使用复合字面值作为初值构造器
```go
s := MyStuct{"tony",18}
a := [5]int{1,2,3,4,5}
sl := []int{1,2,3}
m := map[int]string{1:"aa",2:"bb"}
```

******
# 类型系统

## 指针

**内存地址**
> 内存地址用来定位一段内存
32位占4字节，64位占8字节

## 值部（这个要加深理解）

### Go类型分为两大类别
> Go也可以被看作是C语言的一个扩展框架。 在C中，值的内存结构都是很透明的；但在Go中，对于某些类型的值，其内存结构却不是很透明。 在C中，每个值在内存中只占据一个内存块（一段连续内存）；但是，一些Go类型的值可能占据多个内存块。
> 一个Go值分布在不同内存块上的部分为此值的各个值部（value part）。 一个分布在多个内存块上的值含有一个直接值部和若干被此直接值部引用着的间接值部。

|每个值在内存中只分布在一个内存块上的类型|每个值在内存中会分布在多个内存块上的类型|
|-|-|
|单直接值部|直接值部->底层间接值部|
|布尔类型|切片类型|
|各种数值类型|映射类型|
|指针类型|通道类型|
|非类型安全指针类型|函数类型|
|结构体类型|接口类型|
|数组类型|字符串类型|


## 切片
### 先说数组

+ 数组是固定长度的、容纳同构类型元素的连续序列
+ 数组类型两个属性：元素类型和数组长度
+ 数组是值语义的，**数组的变量表示的是整个数组**
+ 传递数组是纯粹的值copy
+ go中最多的还是使用切片

### 切片说明
+ 切片对于数组相当于文件描述符对于文件
+ 切片是数组的一个操作窗口

切片内部结构（以水壶为例）
+ 地址 （水壶放的位置）
+ 长度 （水壶里面有多少水）
+ 容量 （水壶能装多少水）

### 切片声明和初始化

+ 切片只有一种声明方式，与数组类似，但不指定大小
    + 声明 var 
    + 切片有三种初始化方式
        + 切片作为初始化值
        + 数组作为初始化值
        + make函数返回值作为初始化值

> 注意事项
+ 切片声明后不能直接使用，需要引用到一个数组，或者make初始化，**原因就是切片的零值是nil，nil是没有地址的所以需要初始化才能使用（这样就和上面内置类型零值关联上了）**
+ 不能越界使用

```go
package main

import "fmt"

func main() {
	// 声明 空切片 未初始化
	var s1 []int
	// 空切片 未初始化
	s2 := []int{}
	// 有数据的切片
	s3 := []int{1}
	// // make创建切片，省略cap, cap=len
	s4 := make([]int, 2)
	// // make创建切片，分别定义了len,cap
	s5 := make([]int, 2, 3)
	fmt.Println("s1", s1)
	// fmt.Println("s1内存地址:", &s1[0]) // panic: runtime error: index out of range [0] with length 0
	fmt.Println("s2", s2)
	// fmt.Println("s2内存地址:", &s2[0]) // panic: runtime error: index out of range [0] with length 0
	fmt.Println("s3", s3)
	fmt.Println("s3内存地址:", &s3[0]) // s3内存地址: 0xc0000160a0
	fmt.Println("s4:", s4, "内存地址", &s4[0], "len:", len(s4), "cap:", cap(s4))
	fmt.Println("s5:", s5, "内存地址", &s5[0], "len:", len(s5), "cap:", cap(s5))
}

```

### 切片化

> 这个要理解两个词 slicing，reslicing

+ slicing **切片化** 针对数组 array[low:high]
+ reslicing **切片重组** 针对切片 slice[low:high]

通过切片化数组返回的就是切片了。这里要注意**切片化和切片重组得到的切片**
+ 切片地址 addr &s[low]
+ 长度 len	high-low
+ 容量 cap  array|slice cap - low

### 切片动态扩容
+ 使用append函数追加扩容，让切片类型满足了”零值可用“
+ 尽量使用cap创建切片
+ 当需要的容量超过原切片容量的两倍时，会使用需要的容量作为新容量。
+ 当原切片长度小于1024时，新切片的容量会直接翻倍。而当原切片的容量大于等于1024时，会反复地增加25%，直到新容量超过所需要的容量。

> 切片是数组的描述符，大多数场合代替了数组，减少了数组指针作为函数参数的使用 

## map映射

> map[key]value 不支持零值可用，和切片一样，零值为nil，需要初始化才能使用

### map声明和初始化
+ 声明 var m map[type]type
+ make初始化 m = make(map[type]type, len, cap)
+ 直接创建 m := make(map[type]type, len, cap)
+ 初始化加赋值一起 m := map[type]type {key:value }

### map的基本操作
+ 插入数据 m[k] = v, 如果k存在，那么新值会覆盖旧值
+ 获取个数 len(m)
+ 查找和数据读取 v,ok := m[k]
+ 删除数据 delete(m,"key")
+ 遍历数据 for k, v := range m , **注意：map多次遍历出来的顺序并不相同**

### map扩容

## string字符串

> string类型也是一个描述符，由一个指向底层存储的指针和字符串长度字段组成

+ string类型的数据不可变
+ 零值可用
+ 获取长度的时间复杂度是O(1)级别
+ 通过 + 操作符进行字符串连接
+ 支持比较关系操作符
+ 对非ASCII字符串提供原生支持
+ 原生支持多行字符串 ``

### string声明和初始化
字符串构造
+ 使用fmt.Sprintf
+ 使用strings.Join
+ 使用strings.Builder
+ 使用bytes.Buffer

声明 var s string

初始化 s := "ssss"

### string转换
> string []rune []byte 可以互相转换

## 函数和方法
> go语言中，函数是唯一一种基于特定输入、实现特定任务并反馈任务执行结果的代码块。**本质上，GO程序就是一组函数的集合**
+ 以func关键字开头
+ 支持多返回值
+ 支持具名返回值
+ 支持递归调用
+ 支持同类型的可变参数
+ 支持defer，实现函数优雅返回

### 函数一等公民
> Go中的函数可以像普通整型值那样被创建和使用

+ 正常创建
+ 在函数内创建
+ 作为类型
+ 存储到变量中
+ 作为参数传入函数
+ 作为返回值从函数返回

### defer
+ 拦截panic
+ 修改函数的具名返回值
+ 输出调试信息
+ 还原变量旧值

> 三种defer性能
+ 对于开放编码defer
	+ 编译器会直接将所需的参数进行存储，并在返回语句的末尾插入被延迟的调用
	+ 当整个调用中逻辑上会执行的 defer 不超过 15 个（例如七个 defer 作用在两个返回语句）、总 defer 数量不超过 8 个、且没有出现在循环语句中时，会激活使用此类 defer；
	+ 此类 defer 的唯一的运行时成本就是存储参与延迟调用的相关信息，运行时性能最好
+ 对于栈上分配的defer
	+ 编译器会直接在栈上记录一个 _defer 记录，该记录不涉及内存分配，并将其作为参数，传入被翻译为 deferprocStack 的延迟语句，在延迟调用的位置将 _defer 压入 Goroutine 对应的延迟调用链表中；
	+ 在函数末尾处，通过编译器的配合，在调用被 defer 的函数前，调用 deferreturn，将被延迟的调用出栈并执行；
	+ 此类 defer 的唯一运行时成本是从 _defer 记录中将参数复制出，以及从延迟调用记录链表出栈的成本，运行时性能其次。
+ 对于堆上分配的 defer 
	+ 编译器首先会将延迟语句翻译为一个 deferproc 调用，进而从运行时分配一个用于记录被延迟调用的 _defer 记录，并将被延迟的调用的入口地址及其参数复制保存，入栈到 Goroutine 对应的延迟调用链表中；
	+ 在函数末尾处，通过编译器的配合，在调用被 defer 的函数前，调用 deferreturn，从而将 _defer 实例归还到资源池，而后通过模拟尾递归的方式来对需要 defer 的函数进行调用。
	+ 此类 defer 的主要性能问题存在于每个 defer 语句产生记录时的内存分配，记录参数和完成调用时的参数移动时的系统调用，运行时性能最差。

```go
package main
import (
    "fmt"
)
func d1() {
    for i := 3; i > 0; i-- {
        defer fmt.Print(i, " ")
    }
}

func d2() {
    for i := 3; i > 0; i-- {
        defer func() {
            fmt.Print(i, " ")
        }()
    }
    fmt.Println()
}
func d3() {
    for i := 3; i > 0; i-- {
        defer func(n int) {
            fmt.Print(n, " ")
        }(i)
    }
}
func main() {
    d1()
    d2()
    fmt.Println()
    d3()
    fmt.Println()
}

// 输出结果
1 2 3
0 0 0
1 2 3

```
> defer 是在外围函数返回之后才会执行的。

+ defer会按照顺序放入栈中，然后进先出(LIFO)的原则执行。

+ d1 符合预期

+ d2 defer按顺序放入栈中，等外面函数执行完，再按照(LIFO)执行defer闭包函数，闭包内的执行的时候就会往外部函数找i，所以i 全部都为1

+ d3 defer放入栈中的时候i值确定了，传入进了闭包，所以不需要往外部找i，直接通过参数获取了值

### panic、defer、recover
> panic()是一个内置的Go函数，它终止Go程序的当前流程并开始panicking！ 另一方面，recover()函数也是一个内置的Go函数，允许你收回那些使用了panic()函数的goroutine的控制权。

> 通常写法
```go
defer func() {
		if err := recover(); err !=nil {
			fmt.Println(err)
		}
	}()
```
> 作用域:recover只是针对当前函数和以及直接调用的函数可能产生的panic，它无法处理其调用产生的其他协程的panic

### panic、defer、recover 情况
> 1.一旦运行test2() 函数会导致panic,程序会立即挂掉
```go
package main
 
import (
	"fmt"
)
 
 
func main() {
	test1()       //输出：this is test 1
	test2()       //输出：this is test 2  panic: test 2 is panic   直接挂掉
	test3()                 
}
 
func test1 (){
	fmt.Println("this is test 1")
}
 
func test2 (){
	fmt.Println("this is test 2")
	panic("test 2 is panic")
}
 
func test3 (){
	fmt.Println("this is test 3")
}
 
 
```
> 2.当我们在test2() 函数加入recover()时，程序运行到test2()函数，报panic 错误不会挂掉，程序会继续进行，执行test()3函数。

```go
package main
 
import (
	"fmt"
)
 
 
func main() {
	test1()   //输出：this is test 1
	test2()   //输出：this is test 2  test 2 is  panic
	test3()   //输出：this is test 3
}
 
func test1 (){
	fmt.Println("this is test 1")
}
 
func test2 (){
	defer func() {
		if err := recover(); err !=nil {
			fmt.Println(err)
		}
	}()
	fmt.Println("this is test 2")
	panic("test 2 is panic")
}
 
func test3 (){
	fmt.Println("this is test 3")
}
 
 
```
> 3.当我们把 recover() 放在 直接调用的test2()的main 函数之中时，当程序执行到test2函数时，报panic 这时test2()程序中断，程序不会往下执行，而是直接执行defer 中的recover()函数（同时说明，即使程序某个位置报了panic错误，最后也会执行defer），整个程序不会挂掉。
```go
package main
 
import (
	"fmt"
)
 
 
func main() {
	defer func() {
		if err := recover(); err !=nil {
			fmt.Println(err)
		}
	}()
	test1()    //输出： this is test 1
	test2()    //输出： this is test 2; test 2 is panic
	test3()    //不会执行
}
 
func test1 (){
	fmt.Println("this is test 1")
}
 
func test2 (){
	fmt.Println("this is test 2")
	panic("test 2 is panic")
}
 
func test3 (){
	fmt.Println("this is test 3")
}
 
 
```
> 4.当为test2（）开了个go 协程时，程序依然会报panic 导致整个程序挂掉。
```go
package main
 
import (
	"fmt"
)
 
 
func main() {
 
	defer func() {
		if err := recover(); err !=nil {
			fmt.Println(err)
		}
	}()
	
	test1()
	go test2()
	test3()
	for {
		select {
 
		}
	}
}
 
func test1 (){
	fmt.Println("this is test 1")
}
 
func test2 (){
	fmt.Println("this is test 2")
	panic("test 2 is panic")
}
 
func test3 (){
	fmt.Println("this is test 3")
}
 
 
```
> 5.当为test2()开了个协程时，正确的做法是 在recove()，放在test2()里面才不会导致整个程序挂掉。
```go
package main
 
import (
	"fmt"
)
 
 
func main() {
 
	test1()     // 输出：this is test 1
	go test2()  //  this is test 2; test 2 is panic
	test3()     //this is test3
	for {        //不推荐这样写 会造成死锁  此处只是单单为了 演示
		select {
 
		}
	}
}
 
func test1 (){
	fmt.Println("this is test 1")
}
 
func test2 (){
	defer func() {
		if err := recover(); err !=nil {
			fmt.Println(err)
		}
	}()
	fmt.Println("this is test 2")
	panic("test 2 is panic")
}
 
func test3 (){
	fmt.Println("this is test 3")
}
 
//输出结果：
// this is test 1
// this is test 3
// this is test 2
// test is panic  
 
```
> 总结
+ 恢复panic必须要recover配合
+ recover必须位于同一goroutine的直接调用链上，否则panic无法恢复
+ 当一个 panic 被恢复后，调度并因此中断，会重新进入调度循环，进而继续执行 recover 后面的代码， 包括比 recover 更早的 defer（因为已经执行过得 defer 已经被释放， 而尚未执行的 defer 仍在 goroutine 的 defer 链表中），或者 recover 所在函数的调用方。

### 变长函数
例子
```go
func (values ...int64) (sum int64)
func (sep string, tokens ...string) string

// Sum返回所有输入实参的和。
func Sum(values ...int64) (sum int64) {
	// values的类型为[]int64。
	sum = 0
	for _, v := range values {
		sum += v
	}
	return
}

// Concat是一个低效的字符串拼接函数。
func Concat(sep string, tokens ...string) string {
	// tokens的类型为[]string。
	r := ""
	for i, t := range tokens {
		if i != 0 {
			r += sep
		}
		r += t
	}
	return r
}
```
调用
```go
package main

import "fmt"

func Sum(values ...int64) (sum int64) {
	sum = 0
	for _, v := range values {
		sum += v
	}
	return
}

func main() {
	a0 := Sum()
	a1 := Sum(2)
	a3 := Sum(2, 3, 5)
	// 上面三行和下面三行是等价的。
	b0 := Sum([]int64{}...) // <=> Sum(nil...)
	b1 := Sum([]int64{2}...)
	b3 := Sum([]int64{2, 3, 5}...)
	fmt.Println(a0, a1, a3) // 0 2 10
	fmt.Println(b0, b1, b3) // 0 2 10
}
```

> Go中所有的函数都可以看作是闭包，这是Go函数如此灵活及使用体验如此统一的原因。
## 方法

> 方法事实上是特殊的函数。方法也常被称为成员函数。 当一个类型拥有一个方法，则此类型的每个值将拥有一个不可修改的函数类型的成员（类似于结构体的字段）。 此成员的名称为此方法名，它的类型和此方法的声明中不包括属主部分的函数声明的类型一致。 一个值的成员函数也可以称为此值的方法。

## 接口

### 接口装箱

## 类型内嵌
+ 在接口类型中嵌入接口类型
+ 在结构体类型中嵌入接口类型
+ 在结构体类型嵌入结构体类型


## 通道

> Go提供了一种独特的并发同步技术来实现通过通讯来共享内存。此技术即为通道。 我们可以把一个通道看作是在一个程序内部的一个先进先出（FIFO：first in first out）数据队列。 一些协程可以向此通道发送数据，另外一些协程可以从此通道接收数据。

### 通道初始化
```go
c := make(chan int)
c := make(chan string, 10)
```

### 通道操作
> 1.调用内置内置函数close来关闭一个通道 close(ch)

传给close函数调用的实参必须为一个通道值，并且此通道值不能为单向接收的。

> 2.往通道发送一个值 ch <- v

> 3.从通道接收一个值 <-ch

> 4.查询一个通道的容量 cap(ch)

> 5.查询一个通道的长度 len(ch)

通道的元素值的传递都是复制过程

## Go并发

### select关键字
> select 允许 goroutine 等待多个通信操作。因此，您从 select 获得的主要好处就是它使您能够使用一个select 块处理多个 channels。因此，您可以在 channels 上进行非阻塞操作。

