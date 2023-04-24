```

  ____       _
 / ___| ___ | | __ _ _ __   __ _
| |  _ / _ \| |/ _` | '_ \ / _` |
| |_| | (_) | | (_| | | | | (_| |
 \____|\___/|_|\__,_|_| |_|\__, |
                           |___/

```


# Go的学习笔记

## 目录

<!-- TOC GitLab -->

* [Go语言入门经典](#go语言入门经典)
  - [Go简介](#go简介)
  - [GO环境配置](#go环境配置)
  - [Go命令](#go命令)
  - [Go](#go)
    + [函数](#函数)
    + [控制流程](#控制流程)
    + [使用结构体和指针](#使用结构体和指针)
  - [创建方法和接口](#创建方法和接口)

<!-- /TOC -->


## Go语言入门经典
**Author** George Ornbo

**Go语言的用途**
- 网络编程
- 系统编程
- 并发编程
- 分布式编程

**开源项目**
- Go-Ethereum
- Terraform
- Kubernetes
- Docker
- Netty
- etcd

本书看了3天,比较的简单

### Go简介
Golang是Google在2007年开发的一种开源编程语言，出自**Robert Griesemer、Rob Pike和Ken Thompson** 在2009年11月10日发布
指出Go的主要目标是”兼具Python等动态语句的开发速度和C或C++等编译型语言的性能与安全性“

Go使用编译器来编译代码。编译器将源代码编译成二进制格式；在编译代码时，编译器检查错误、优化性能并输出可在不同平台上运行的二进制文件。其自带编译器

--------

**<mark>总结：**</mark>
1. 设计Go语言是因为Java和C++等传统语言繁琐，缓慢而难以理解。Go语言借鉴了Python动态类型语言的优点，旨在打造易于使用开发高流量生产系统的语言。
2. 在开发阶段，推荐使用go run；程序开发完毕，可以分享时，建议使用go build 。
3. Go负责分配内存和执行垃圾收集。虽然正常的内存使用规则依然使用，但无须直接管理内存。
4. 在编程中，错误地理解数据类型通常会导致Bug出现。使用数据源前，请花时间搞明白数据类型。如果数据源为数据库，请了解数据库模式（schema）及其使用的数据类型，将节省大量的调试时间。
5. 可将函数作为参数传递给其他函数，函数被视为一种类型，因此可以传递。在Go中，函数是一等公民
6. else if和switch都是定义控制流程的合法方式。相比与使用一系列else if，使用switch语句编写的代码更容易理解，且更快。
7. 一些需要使用defer语句的例子包括：在读取文件后将其关闭、收到来自Web服务器的响应后对其进行处理以及建立连接后向数据库请求数据。需要在某项工作完成后执行特定的函数时，defer语句是不错的选择。并发gorutine中，建立go并发后可以用defer来关闭。
8. 在Go中，使用数组有一定的局限性。无法在数组声明后添加元素；切片比数组更灵活，可以添加、删除和复制元素。可将切片视为轻量级的数组包装器，它保留了数组的完整性，又比数组使用更容易。
9. 除非确定必须使用数组，否则请使用切片。切片能够让您轻松地添加和删除元素，还无须处理内存分配问题，不能用delete用于切片。可使用append来完成删除。
10. 指针和值的差别很微妙，但选择使用指针还是值很容易区分：如果需要修改原始结构体实例，就使用指针；如果要操作一个结构体，但不想修改原始结构体实例，就使用值。
11. 面向对象编程的编程范式：使用具有特定行为的对象来建立数据模型。通常，面向对象语言提供允许一种对象继承另一种对象的功能。虽然Go语言没有提供类和类继承等面向对象元素，但结构体和方法集弥补了这部分而不足，提供了一些面向对象元素。由此可说Go在不使用类和继承的情况下提供了类似于面向对象编程的功能，虽然这点存在争议。
12. 除从技术角度考虑Go语言的错误处理方式和错误生成方式外，还需从以用户为中心的角度考虑错误。编写供他人使用的库或包时，您编写和使用的错误的方式将极大的影响可用性。
13. 不同于Java等其他语言，Go不支持传统的try-catch-finally控制结构，而向函数或方法的调用者报告错误。Go语言将错误作为返回值，这只是它做出的一种设计决策，但对这种处理错误的方式仍有争议。
14. Node.js使用事件来循环管理并发，而Java使用线程。Apache喜欢用线程和进程,Nginx使用事件循环。与Java一样，Go在幕后使用线程来管理并发，让程序员无须之间管理线程，它消除了这样做的痛苦。创建一个Goroutine只需要占用几kb的内存，因此创建和销毁的效率也非常高。其是一个并发抽象，无须准确知道操作系统中发生的情况。
15.


<mark> **拓展:**</mark>
1. 观看Gary Bernhardt的讲解视频WAT。该视频谈论了包括JavaScript在内的动态类型语言。切忌不分青红皂白地全盘接受。
2. 斯坦福大学教授Mehran Sahami的讲座探索了内存工作的原理。虽然该讲座针对的时Java，但大部分内容适用于Go。
3. 阅读Go的包。例如：fmt，strings，errors，strconv, buffer,
4. 深入处理错误类型:阅读Rob Pike的博文《Errors are Values》
5.


--------

### GO环境配置
```
mkdir $HOME/go
mkdir $HOME/go/bin
mkdir $HOME/go/pkg
mkdir $HOME/gosrc
```
配置zshrc或bashrc
下面是我个人的配置
```
#Go
export GOPATH=$HOME/go
export GOROOT=/usr/lib/go
export GOBIN=$HOME/go/bin
export PATH=$PATH:$GOPATH:$GOROOT:$GOBIN:$GOPROXY
#export GO111MODULE=on
export GO111MODULE=auto
#go代理
#export GOPROXY=https://goproxy.io
export GOPROXY=https://goproxy.cn
```

### Go命令
- go run - 直接编译并运行文件，不会创建可执行文件
- go build - 编译成二进制可执行文件，可对应不同的平台
- 可以指定操作的系统环境来设置特定的编译目标，类似GOOS和GOARCH来指定是Win、Linux、Mac和amd、x86、arm


### Go

Go是一种静态类型语言，

**强类型语言**指的是错误地使用了类型时，编译器将引发错误；

**动态类型（松散或弱)** 指的是为了执行程序，运行时会将一种类型转换为另一种类型，或者编译器没有实现类型系统。

计算机科学家看重强类型语言的正确性和安全性，而其他人则看重动态语言的简单性和开发速度。

**静态语言的优点**
- 性能高于动态类型语言
- Bug通常会被编译器发现
- 代码编辑器可提供代码补全和其他功能
- 数据完整性更好

**动态语言的优点**
- 使用动态类型语言编写软件度速度通常更快
- 无须为执行代码而等待编译器完成编译
- 变更代码容易
- 学习门槛低

在Go中，程序员可以显示地声明类型，也可让编译器推断类型。


**类型**

Go语言中必须声明布尔变量
```go
//布尔类型
var b bool
```
如果没有给布尔变量复制，它将默认为false。

**数值类型**

```go
//整数
var i int = 3
```
可正可负,若要处理的数很大才需要特别声明

```go
//浮点数
var f float32=0.111
```
```go
//字符串
var s string="foo"
```
可以为空，适合用来累积其他变量中的数据以及存储临时数据。
可将其他数据相加，但不能修改原来的值。
不能对字符串执行数学运算，必须先将其转换为数字类型。

数组
声明数组时，必须指定其长度和类型
```go
var beatles [4]string
```

注意：数组索引从0开始

检查变量的类型 - reflect包

```go
package main
import(
"fmt"
"reflect"
)
func main(){
  var s sting="string"
  fmt.Println(reflect.TypeOf(s))
}

```

类型转换 - strconv包
提供了一整套类型转换方法，可用于转换为字符串或将字符串转换为其他类型。
```go
var s string = "true"
b,err:=strconv.ParseBool(s)
```

**变量**
变量就是值的引用，是实现程序逻辑的基石之一。
Go是一种静态类型语言，因此声明变量必须显示或隐式地指定其类型

使用关键字var声明

```go
//string
var s string="Helo world"
//int
var i int=6
//可以先声明后赋值
```

将类型不正确的值赋值给变量时，将导致编译错误
打印值使用fmt包
```go
fmt.Println(s)
```
**快捷变量**

```go
//可在一行内声明多个类型相同的变量并给它们赋值
var s, t string="helo", "world"

//对于不同类型的变量

var(
  s string="helo"
  i int=6
  )
```
声明变量后，不能再次声明它。可以重新赋值变量，但不能重新声明变量，否则将导致编译阶段错误。

在Go语言中，声明变量时若未赋值，则为默认值零值，变量的默认值取决于其类型。

```go
var i int
var f float
var b bool
var s string
fmt.Println("%v %v %v %q\n", i, f, b, s)
// 输出 0 0 false ""
```
确定变量是否已经赋值，不能检查它是否为nil，而必须检查它是否为默认值。

简短变量声明

```go
func main(){
s:="helo world"}
//必须在函数中才能使用简短声明，编译器会推断变量的声明，无需显示指定变量的类型。
```

**类型声明的方式**

```go

var s string="helo world"
var s ="helo world"
var s string
s="helo world"
s:="helo world"
```


**类型推导**

```go
var {
a = 1
s = "string"
c = 1.1
d = false
}

```

--------

**变量作用域**

Go语言使用基于块的词法作用域
- 块是位于一对大括号内的一系列声明和语句，可以为空
- {}表示一个块
- 在{}内声明的变量，可在相应块的任何地方访问
- {}内部定义了一个新块{{}} -> 内部块
- 在内部块中，可访问外部块中声明的变量，可引用外部块的变量，但外部块不能访问内部块
- 代码的缩进程度反映了块作用域的层级。
- Go语言将文件也视为块，所以在第一级{}外声明的变量可在所有块中访问

**指针**

同C语言大致相同，在Go语言中声明变量时，将在计算机内存中给它分配一个位置，以便能够存储、修改和获取变量的值。要获取变量在计算机内存中的地址，可在变量名前加上&字符。
就是C语言中的解引用
声明用\*字符

```go

i:=*int 1
fmt.Println(&i)
//打印i的内存地址
fmt.Println(*i)
//打印i的值
```


**声明常量**

```go
//常量初始化后，可以引用它，但不能修改。
const greeting string = "Helo world"
```


#### 函数

```go
//函数的结构
func function_Name(x type,y type)return_type{
  return
}
//如果函数签名声明了返回值，则函数必须以终止语句结束。通常有一个返回值，但并非总是如此。
```


设计函数时该考虑的因素
- 让每个函数只做一件事并做好。软件不可避免地要修改，通过结合使用大量简短的函数，可让软件更容易修改。还有助于测试各个函数以及整个软件。
- 维护。编写的函数易于阅读和理解，过于复杂需要添加注释。
- 性能。
- 调用函数，可通过名称对其进行引用，并提供所需参数。
- 可在函数签名中声明多个返回值，让函数返回多个结果。在这种情况下，终止语句可返回多个值。

```go
//示例
func getPrice()(int, string){
  i:=2
  s:="Helo World"
  return i, s
  }
```


**定义不定参数**
不定参数函数是参数数量不确定的函数。它们接受可变数量的参数。
在Go语言中，能过传递可变数量的参数，但它们的类型必须与函数签名指定的类型相同。要指定不定参数，可使用3个(...)

```go
func sumNumbers(numbers...int)int{
  total:=0
  for _, numbers:=ranger numbers{
    total += number
  }
  return total
}
```


**具名返回值**
具名返回值让函数能够在返回前将值赋给具名变量，真有助于提升函数的可读性，使其功能更加明确。要使用具名返回值，可在函数签名的返回值部分指定变量名。

```go
func sayHi()(x, y, string){
  x="helo"
  y="world"
  return
  /*这个函数体中，在终止语句return前给具名变量进行了赋值。使用具名返回值时，无须显示地反回相应的变量。被称为裸（naked）return语句。
  按声明的顺序返回
  */
}

```


**递归函数**

递归函数是不断调用自己直到满足特定条件的函数。要在函数中实现，可将调用自己的代码作为终止语句中的返回值。

**将函数作为值传递**
Go将函数视为一种类型，因此可将函数赋给变量，以后再通过变量来调用它们。


```go
//将函数作为值传递
func main(){
fn := func(){
    fmt.Println("function called")
    }
  fn()
}
//将函数作为参数传递
func anotherFunction(f func() string) string{
  return f()
}
func main(){
fn := func(){
    fmt.Println("function called")
    }
  fmt.Println(anotherFunction(fn))
}
```

#### 控制流程



```go
// if 语句
if a {
  fmt.Println("onli if ")
  }
// if-else 语句
if b {
  fmt.Println("if")
}else{
  fmt.Println("else")
  }
// if-elseif-else 语句
if c1 {
  fmt.Println("if")
}else if c2 {
  fmt.Println("else if")
}else{
  fmt.Println("else")
}
//else if 语句能让前面为false时接着判断后面的布尔表达式，可多个嵌套，else会在到达时直接执行
```

**运算符**
- 比较运算符
- 算术运算符
- 逻辑运算符

| 比较字符 | 运算符   |
|----------|----------|
| ==       | 等于     |
| !=       | 不等于   |
| <        | 小于     |
| <=       | 小于等于 |
| >        | 大于     |
| >=       | 大于等于 |


| 算术字符 | 运算符 |
|----------|--------|
| +        | 加     |
| -        | 减     |
| *        | 乘     |
| /        | 除     |
| %        | 模     |

| 逻辑字符 | 运算符                           |
|----------|----------------------------------|
| \&\&     | 与:两个条件是否都为True          |
| \|\|     | 或：两个条件是否至少有一个为True |
| \!       | 非:条件是否为false               |


**使用switch语句**
switch语句可用来替代冗长的if else布尔比较，从编译层面上说，这样的代码效率也更高。

```go
func main(){
  i:=2
  switch i {
    case 2:
      fmt.Println("Two")
    case 3:
      fmt.Println("Three")
    default://若case不满足则执行，位置通常放最后
      fmt.Println("helo world")
  }
}
```

For**循环**
在Go中，只用for来执行循环语句，没有while等等

```go
func main(){
  i:=0
  for i<10 {
    i++
    fmt.Println("i is ", i)
  }
}
//包含初始化语句和后续语句的for语句
for i:=0; i<10; i++{
  fmt.Println("i is ", i)
}
//包含range子句的for语句
numbers:=[]int{1, 2, 3, 4}
for i, n:=ranger numbers{
  fmt.Println("The index of the loop is", i)
  fmt.Println("The value from the array is", n)
}
```


在Go语言中，可使用包含range子句的for语句来遍历大多数据结构，且无须知道数据结构的长度。

**defer语句**

defer语句能够让您在函数返回前执行另一个函数。函数在遇到return语句或到达函数末尾时返回。defer语句通常用于执行清理操作或确保操作（如网络调用)完成后再执行另一个函数。

defer延迟执行执行的时机是遇到错误或者return前。多条defer语句按栈执行，后进先出。

**数组、切片和映射**

数组是一个数据集合，在编程中它通常按逻辑对数据进行分组。数组也是基本的编程构件，常用于存储一系列用数字索引的数据。


```go
//要创建数组，可声明一个数组变量，并指定其长度和数据类型
var cake [4]string
//赋值，索引从0开始
cake[0]='helo'
cake[1]='world'
//打印数组值
fmt.Println(cake[0])
//打印数组的所有元素，可使用变量名本身
fmt.Println(cake)
```
声明数组的长度后，就不能给它添加元素了。否则导致编译阶段错误。


**切片**

在Go中，数组是一个重要构件，但使用切片的情况更多。切片是底层数组中的一个连续片段，通过它可以访问数组中一系列带编号的元素。能够让你顺序访问数组的特定部分。

```go
//声明切片，使用Go的内置函数make创建一个切片，第一个参数为数据类型，第二个是长度。
var cake = make([]string, 2)
//打印同数组相同
//添加元素 使用内置函数append
cake := append(cake, "helo")
```

append会在必要时调整切片的长度，但对程序员隐藏了这种复杂性。在编程接口方面，程序员只需使用新创建的索引来引用这个元素即可。

append也是一个不定参数函数。意味可在切片末尾添加很多值。
> cake := append(cake, "world","Redari-Es","Happy")

删除元素,也可使用内置函数append。
> cake = append(cake[:2], cake[2+1:]...)

要复制切片的全部或部分元素，可使用内置函数copy。在复制切片中的元素前，必须再声明一个类型与该切片相同的切片


```go
var bigcake = make([]string, 3)
bigcake[0]="first"
bigcake[1]="second"
bigcake[2]="third"
var smallcake = make([]string, 2)
copy(smallcake, bigcake)
//在新切片中创建元素的副本，修改一个切片中的元素不会影响另一个切片。还可将单个元素或特定范围内的元素复制到新切片中
copy(smallcake, bigcake[1:])
```

**映射**

数组和切片是可以通过索引值访问的元素集合，而映射是通过键来访问的无序元素编程。在其他编程语言中，映射也被称为关联数组、字典或散列。映射在信息查找方面的效率非常高，因为可直接通过键来检索数据。简单地说，映射可视为键-值对集合。
> var cake = make(map[string]int)

可在映射中动态地添加元素，而无须调整映射的长度。这是Go语言更像Ruby和Python等动态语言。

要从映射中删除元素，可使用内置函数delete
> delete(cake,"key")

使用内置函数make创建映射时，可使用第二个参数，但这个参数只是容量提示，而非硬性规定。映射可根据要存储的元素数量自动增大，因此没有必要指定长度。

#### 使用结构体和指针
<++>

结构体是由数据元素组成的结构，它是一个很有用的编程构件。

结构体是一系列具有指定数据类型的数据字段，它能够让您通过单个变量引用一系列相关的值。通过使用结构体，可在单个变量中存储众多类型不同的数据字段。存储在结构体中的值可轻松地访问和修改，这提供了一种灵活的数据结构创建方式。通过使用结构体，可提高模块化程度，还能够创建并传递复杂的数据结构。



```go
type Move struct {
  Name string
  Rating float32
}
func main(){
m := Movie{
  Name: "Citizen",
  Rating: 10,
}
}
//声明结构体后，可通过多种方式创建它。声明后，可直接声明这种类型的变量
var m Movie
//要调试或查看结构体的值，可使用fmt包将结构体的字段名和值打印出来。
fmt.Printf("%v\n", m)
//创建结构体时，如果没有初始化，则每个数据字段设置为相应数据类型的零值
//可用点表示法给其字段复制
var m Movie
m.Name="helo"
m.Rating=0.88
//可使用关键字new来创建结构体实例，为其分配内存；
m := new(Movie)
m.Name="world"
m.Rating=0.5
//还可使用简短变量赋值来创建结构体，可省略new。可同时给字段复制，方法是使用字段名、冒号和字段值
c:=Movie{Name:"Helo",Rating:10}
//也可省略字段名，按字段声明顺序给它们赋值，但出于可维护性，不推荐
```

使用简短变量赋值是最常用的结构体创建方式

**类C语言也支持结构体**
结构体并非创建面向对象代码的方式，而是一种数据结构创建方式，旨在满足数据建模需求。

**嵌套结构体**

有时候，数据结构需要包含多个层级。此时可用切片等数据类型，但需要的结构更复杂。嵌套是更有用的方式。

```go
type Superhero struct{
  Name string
  Age int
  Address Address
}
type Address struct{
  Number int
  Street string
  City string
}
func main(){
  e:=Superhero{
    Name:"Batman",
    Age: 32,
    Address: Address{
      Number:1007,
      Street:"Mountain Drive",
      City: "Gotham",
    },
  }
fmt.Printf("%+v\n", m)
}
```

**自定义结构体数据字段的默认值**


| 类型            | 零值  |
|-----------------|-------|
| 布尔性(Boolean) | false |
| 整形(Integer)   | 0     |
| 浮点性(Float)   | 0.0   |
| 字符串(String)  | " "   |
| 指针(Pointer)   | nil   |
| 函数(Function)  | nil   |
| 接口(Interface) | nil   |
| 切片(Slice)     | nil   |
| 通道(Channel)   | nil   |
| 映射(Map)       | nil   |

Go语言没有提供自定义默认值的内置方法，但可使用构造函数来实现。构造函数创建结构体，并将没有指定值的数据字段设置为默认值。


```go
type Alarm struct{
  Time string
  Sound string
}
func NewAlarm(time string) Alarm{
a:=Alarm{
  Time:time,
  Sound:"Beef"
  }
  return a
}
```

**比较结构体**
对结构体进行比较，先看它们的类型和值是否相同。
不能对两个类型不同的结构体进行比较，否则将导致编译错误。因此，试图比较两个结构体之前，必须确定它们的类型相同。可使用reflect包
> fmt.Printf(reflect.TypeOf(a))


**公有和私有值**
如果一个值被导出，可在函数、方法或包外面使用，它就是公有的；如果一个值只能在其所属上下文中使用，那它是私有的。

Go语言规定，结构体及其数据字段都可能被导出，如果一个标识符的首字母是大写，那么它将被导出；否则不会。要导出结构体及其字段，结构体及其字段名称都必须以大写字母开头。

**区分指针引用和值引用**
同C指针相同
数据值存储在内存中，指针包含值的内存地址，意味使用指针可读写存储的值；


```go
/*创建结构体实例，给数据字段分配内存并给它们指定默认值；
然后返回指向内存的指针，并将其赋给一个变量。
使用简短变量赋值时，将分配内存并指定默认值。
*/
type Drink struct{
  Name string
  Ice bool
}
func main(){
  a:=Drink{
    Name:"Coke",
    Ice:true,
    }
  b:=a
  b.Ice=false
  fmt.Printf("a:%+v\n", a)
  fmt.Printf("b:%+v\n", b)
  fmt.Printf("a:%+v\n", &a)
  fmt.Printf("b:%+v\n", &b)
}
```

### 创建方法和接口
<++>
方法类似于函数，但有一点不同：在关键字func后面添加了另一个参数部分，用于接受单个参数。

请注意，在方法声明中，关键字func后面多了一个参数——接收者。严格地说，方法接收者是一种类型，指向结构体的指针。接下来是方法名、参数以及返回值。

```go
type Moive struct{
  Name string
  Rating float32
}
//方法
func (m *Movie) summary()string{}
//函数等同上面
func summary(m *Movie)string{}

```


如果使用函数，则在每个使用函数或结构体的地方，都需要包含函数和结构体的定义，这会导致代码重复。另外，函数发生任何改变，都必须修改多个地方。这样看来在函数与结构体关系密切时，用方法更合理。
使用方法的优点在于，只需编写方法一次，就可对结构体的任何实例进行调用。


```go
//方法示例
package main

import (
  "fmt"
  "strconv"
)

type Movie struct {
  Name   string
  Rating float64
}

func (m *Movie) summary() string {
  r := strconv.FormatFloat(m.Rating, 'f', 1, 64)
  return m.Name + "," + r
}

func main() {

  m := Movie{
    Name:   "Spiderman",
    Rating: 4.5,
  }
  fmt.Println(m.summary())
}
```

**创建方法集**
方法集是可对特定数据类型进行调用的一组方法。在Go中，任何数据类型都可有相关联的方法集，这让你能够在数据类型和方法之间建立关系。方法集可包含的方法数量不受限制，这是一种封装功能和创建库代码的有效方式。


```go
package main

import (
  "fmt"
  "math"
)

func main() {
  s := Sphere{
    Radius: 5,
  }
  fmt.Println(s.SurfaceArea())
  fmt.Println(s.Volume())
}

type Sphere struct {
  Radius float64
}

func (s *Sphere) SurfaceArea() float64 {
  return float64(4) * math.Pi * (s.Radius * s.Radius)
}
func (s *Sphere) Volume() float64 {
  radiusCubed := s.Radius * s.Radius * s.Radius
  return (float64(4) / float64(3)) * math.Pi * radiusCubed
}

```


**使用方法和指针**
与结构体一样，方法是一个接受被称为接收者的特殊参数的函数，接收者可以是指针，也可是值。

同样：如果需要修改原始结构体，就使用指针；如果需要操作结构体，但不想修改原始结构体，就使用值。


**接口**
在Go中，接口指定了一个方法集，这是实现模块化的强大方式。可将接口视为方法集的蓝本，它描述了方法集中的所有方法，但没有实现它们。它充当了方法集规范，意味者可在符合接口要求的前提下随便更换实现。

通过使用接口，可将代码重用于相同行为的实体。


```go
//接口示例
package main

import (
  "errors"
  "fmt"
)

func main() {
  t := T850{
    Name: "The Terminato",
  }
  r := R2D2{
    Broken: true,
  }
  err := Boot(&r)
  if err != nil {
    fmt.Println(err)
  } else {
    fmt.Println("Robot is powered on!")
  }
  err = Boot(&t)
  if err != nil {
    fmt.Println(err)
  } else {
    fmt.Println("Robot is powered on!")
  }

  fmt.Println("hello world")
}

type Robot interface {
  PowerOn() error
}
type T850 struct {
  Name string
}

func (a *T850) PowerOn() error {
  return nil
}

type R2D2 struct {
  Broken bool
}

func (r *R2D2) PowerOn() error {
  if r.Broken {
    return errors.New("RR2D2 is broken")
  } else {
    return nil
  }
}
func Boot(r Robot) error {
  return r.PowerOn()
}

```


接口提供的抽象层可能有点复杂，但有助于代码的重用，还能完全更换实现。
通过定义一个接口，该接口的实现比使用的数据库更重要。理论上，只要实现满足接口的要求，就可以使用任何数据库,因此可轻松更换数据库，接口可包含多个实现，引入了多态的概念。

多态意味者多种形式，让接口能够有多种实现。在Go中，接口以声明的方式提供了多态，因为接口描述了必须提供的方法集以及这些方法的函数签名。如果一个方法集实现了一个接口，就可以说它与另一个实现了该接口的方法集互为多态。编译器也会验证接口：检查方法集并确保接口确实是多态的。通过将接口正式化，可确保接口的两种实现是多态的，让代码可验证、可测试且是灵活的。

可在接口的实现中添加额外的方法，但这仅适用于结构体，而不使用于接口。


**使用字符串**

Go语言支持两种创建字符串字面量的方式。解释型字符串字面量是用双引号括其的字符。
> s:="I am an interpreted string literal"


《Go语言规范》
| rune字面量 | Unicode字符                            |
|------------|----------------------------------------|
| \a         | alert or bell                          |
| \b         | 退格                                   |
| \f         | 换页符                                 |
| \n         | 换行符                                 |
| \r         | 回车                                   |
| \t         | 水平制表符                             |
| \v         | 垂直制表符                             |
| \\ \\      | 反斜杠                                 |
| \'         | 单引号，转义序列只能包含在rune字面量中 |
| \"         | 双引号，转义序列只能包含在rune字面量中 |


通过使用rune字面量，可将解释型字符字面量分成多行，还可在其中包含制表符和其他格式选项。

原始字符串字面量用**反引号括起**。不同于解释型字符串，原始字符串中的反斜杠没有特殊含义，Go按原样解释这种字符串。

**拼接字符串**
用运算符+来拼接字符串变量
> s:="helo"+" world"

还可用复合赋值运算符+=来拼接字符串变量
> s:="helo"
> s+=" world"

不能拼接不同类型的变量，可使用strconv包中的方法Itoa来完成，它将整数转换为字符串。


```go
//Itoa
package main

import (
  "fmt"
  "strconv"
)

func main() {
  var i int = 1
  var s string = " egg"
  inToString := strconv.Itoa(i)
  var breakfast string = inToString + s
  fmt.Println(breakfast)
}
```

**使用缓冲区来拼接字符串**

对于简单而少量的拼接，使用运算符虽然很好，但随着操作次数的增加，这种效率并不高。如果需要在循环中拼接，使用空的字节缓冲区来拼接的效率更高。

```go
//Buffer
package main

import (
  "bytes"
  "fmt"
)
func main() {
  var buffer bytes.Buffer
  for i := 0; i < 500; i++ {
    buffer.WriteString("z")
    fmt.Println(buffer.String())
  }
}
```


Go语言的两位设计者Rob Pike和Ken Thompson也是UTF-8的联合设计者
Go语言支持UTF-8和国际字符集
Go源代码也是UTF-8de


要更深入地理解字符串以及如何操作它们，必须首先知道Go语言中的字符串实际上是只读的字节切片。要获悉字符串包含多少个字节，可使用Go语言的内置函数len

```go
s:="helo"
fmt.Printf(len(s))
//outputs 4
//可输出特定位置的字节值
fmt.Printf(len(s[0]))
//outputs 104
```
由于通过索引访问字符串时，访问的是字节不是字符，因此显示的是以十进制表示的字节值。

可使用格式设置将十进制转换为字符和二进制表示
```
s:='helo'
fmt.Println("%q", s[0])
// outputs 'h'
fmt.Println("%b", s[0])
// outputs 1101000
```


| 格式符 | 输出     |
|--------|----------|
| %q     | 字符     |
| %b     | 二进制数 |
| %d     | 十进制   |


**处理字符串**
给字符串变量赋值后，可使用标准库中的strings包提供的方法

将字符串转换为小写
> fmt.Println(strings.ToLower("VERY IMPORTANT MESSAGE"))


查找字符串
提供了index方法
> fmt.Println(strings.Index("surface", "face"))

将返回其索引

删除字符串中的空格

> fmt.Println(strings.TrimSpace(" I don't need all this space "))



**处理错误**

软件不可避免地会有错误及遇到未考虑的情形，很多语言选择在发生必须捕获的错误时引发异常，而Go语言处理错误的方式是将其作为一种类型，意味着可将错误传递给函数和方法。

在Go中，一种约定是在调用可能出现问题的方法或函数时，返回一个类型为错误的值。这意味这如果出现问题，函数通常不会引发异常，而让调用者决定如何处理错误。

```go
//erro
package main

import (
  "fmt"
  "io/ioutil"
)
/*ReadFile接受一个字符串参数，并返回一个字节切片和一个错误值。
func ReadFile(filename string) ([]byte,error)
意味着总是会返回一个错误值，可对其检查
*/
func main() {
  file, err := ioutil.ReadFile("ctf.txt")
  /*简短声明等价于
    var file []byte
    var err error
    file,err=ioutil.ReadFile("ctf.txt")
  */
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println("%s", file)
}
```

在Go语言中，有一种约定是，如果没有发生错误，返回的错误值将为nil。所以经常用于执行检查

```go
if err!=nil{
  //something went wrong
}
```

在Go中，错误是一个值。标准库声明了接口error

```go
type error interface{

  Error() string
}
//这个接口只有一个方法——Error，它返回一个字符串
```

```go
//创建并打印错误
func main(){
  err:=errors.New("Something went wrong")
        if err!=nil{
          fmt.Println(err)
        }
}
```

除errors包外，标准库中的fmt包还提供了Errorf，可用于设置返回的错误字符串的格式。

```go
//fmt.Errorf
func main() {
  name, role := "Richard Jupp", "Drummer"
  err := fmt.Errorf("The %v %v quit", role, name)
  if err != nil {
    fmt.Println(err)
  }
}
```
**从函数返回错误**


错误处理不是在函数中，而是在调用函数的地方进行的。这在错误处理方面提供了极大的灵活性，而不是简单地一刀切。

```go
//return err from func
func Half(numberToHalf int) (int, error) {
  if numberToHalf%2 != 0 {
    return -1, fmt.Errorf("Cannot half %v", numberToHalf)
  }
  return numberToHalf / 2, nil
}
func main() {
  n, err := Half(19)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(n)
}
```

**慎用panic**
panic是Go中的一个内置函数，它终止正常的控制流程并引发恐慌（panicking），导致程序停止执行。出现普通错误时，不提倡用它，因为程序将停止执行，且没有任何回旋余地。

```go
//panic
func main() {
  fmt.Println("This is executed")
  panic("Oh no.I can do no more. Goodbye.")
  fmt.Println("This is not executed")
}
```

当程序处于无法恢复的状态，通常终止程序，避免出现更多的错误
```go
if err!=nil{
  panic(err)
}
```

在Go语言中，可从函数返回多个值，一种约定是将错误作为最后一个返回值。这样可自定义错误并将其返回给调用者，有调用这决定如何处理错误。其他语言认为，不管发生什么错误，都应让程序立即崩溃；而Go语言更灵活，让方法或函数的调用者决定如何处理错误。


**使用Goroutine**

并发和并行
前者同时处理很多事情，后者同时做很多事情。
一个人做很多事，多个人做一件事


```go
//模拟阻塞的函数调用
package main
import (
  "fmt"
  "time"
)
func slowFunc() {
  time.Sleep(time.Second * 2)
  fmt.Println("sleeper() finished")
}
func main() {
  //go slowFunc()
  slowFunc()
  fmt.Println("I am not shown until slowFunc() completes")
}
```

并发地执行代码意味着程序可能能够更快地执行完毕，并在数据就绪后就返回它，而无须等待程序其他部分结束。


**通道**

通道是一种与Goroutine通信的方式。通道让数据能够进入和离开Goroutine，可方便其相互通信。《Effective Go》说明了Go语言的并发理念：**“不要通过共享内存来通信，而通过通信来共享内存”**

在其他编程语言中，并发编程通常是通过在多个进程或线程之间共享内存实现的，共享内存能够让程序同步，确保程序以合乎逻辑的方式执行。在执行过程中，进程或线程可能对共享内存加锁，以禁止被其他进程修改，这会引发Bug或崩溃。通过这种方式给内存加锁，可确保它是独占的即只有一个进程或线程能够访问它。

Go使用通道在Goroutine之间收发信息，避免了使用共享内存。严格地说，Goroutine并不是线程，但可视为线程，因为它们能够以非阻塞方式执行代码。

上一个示例使用计时器来管理并发，在高并发中，累积的计时器也许会变大，在更复杂的并发中并非好的方式。通道让Goroutine结束时就能够告诉主程序。
> c:=make(chan string)

string指出通道将用于存储字符串数据
这意味着这个通道只能用于收发字符串值

向通道发送消息
> c <- "Helo world"

其中的<-,表示将右边的字符串发送给左边的通道。

从通道接收消息
> msg := <-c


make函数是Go的内置函数，其作用是为slice、map或chan初始化并返回引用。

*要从通道那里接收消息，需要在<-后面加上通道名。可使用简短变量赋值，将来自通道的消息直接赋给变量。箭头向左表示数据离开通道（接收），箭头向右表示进入通道（发送）。*

```go
//chan
func main() {
  c := make(chan string)
  go slowFunc(c)
  msg := <-c
  fmt.Println(msg)
}
func slowFunc(c chan string) {
  time.Sleep(time.Second * 2)
  c <- "slowFunc() finished"
}
```

**使用缓冲通道**
通常，通道收到消息后就可将其发送馆接收者，但有时可能没有接收者。这种情况向，可使用缓冲通道。缓冲意味者可将数据存储在通道中，等待接收者就绪再交付。要创建缓冲通道，可向内置函数make传递另一个表示缓冲区长度的参数。
> message := make(chan string, 2)

指创建一个可存储两条消息的缓冲通道。请注意，缓冲通道最多只能存储指定数量的消息。

```go
//chan buffer close receiver
func receiver(c chan string) {
  for msg := range c {
    fmt.Println(msg)
  }
}
func main() {
  messages := make(chan string, 2)
  messages <- "helo"
  messages <- "world"
  close(messages)
  fmt.Println("Pushed two messages onto Channel with receivers")
  time.Sleep(time.Second * 2)
  receiver(messages)
  fmt.Println("hello world")
}
```

close用来关闭通道，禁止再向通道发送消息。

**阻塞和流程控制**

Goroutine会立即返回（非阻塞），因此要让进程处于阻塞状态必须采用一些流程控制技巧。

给通道指定消息接收者是一个阻塞操作，因为它将阻塞函数返回，直到收到一条消息为止。

```
//通道和流程控制
func pinger(c chan string) {
  t := time.NewTicker(1 * time.Second)
  for {
    c <- "ping"
    <-t.C
  }
}
func main() {
  messages := make(chan string)
  go pinger(messages)
  msg := <-messages
  fmt.Println(msg)
}
```

通过使用for语句，可永久性地阻塞进程，也可让阻塞时间持续特定的迭代次数。


```go
//通道和流程控制，for永久迭代
func pinger(c chan string) {
  t := time.NewTicker(1 * time.Second)
  for {
    c <- "ping"
    <-t.C
  }
}
func main() {
  messages := make(chan string)
  go pinger(messages)
  for {
    msg := <-messages
    fmt.Println(msg)
  }
}
```

**将通道用作函数参数**
可将通道作为参数传递给函数，并在函数中向通道发送消息。要进一步指定在函数中如何使用传入的通道，可在传递通道时将其指定为只读、只写或读写的。

<-位于关键字chan左边时，表示通道在函数内是只读的；
> func channelReader(messages <-chan string)

<-位于关键字chan右边时，表示通道在函数内是只写的；
> func channelReader(messages chan<- string)

没有指定<-时，表示通道在函数内是读写的；
> func channelReader(messages chan string)


通过指定通道访问权限，有助于确保通道中数据的完整性，还可指定程序的哪部分可向通道发送数据或接收来字通道的数据。


**select语句**
它为通道创建一系列接收者，并执行最先收到消息的接收者。

```go
channel1:=make(chan string)
channel2:=make(chan string)
select{
  case msg1:=<-channel1:
    fmt.Println("received", msg1)
  case msg2:=<-channel2:
    fmt.Println("received", msg2)
}
```

具体执行哪条case语句，取决于消息到达的时间哪条消息最先到达决定了将执行哪条case语句。通常，接下来收到的其他消息将被丢弃。收到一条消息后，select语句将不再阻塞。



```
//select
func ping1(c chan string) {
  time.Sleep(time.Second * 1)
  c <- "ping on channel1"
}
func ping2(c chan string) {
  time.Sleep(time.Second * 2)
  c <- "ping on channel2"
}
func main() {
  channel1 := make(chan string)
  channel2 := make(chan string)
  go ping1(channel1)
  go ping2(channel2)
  select {
  case msg1 := <-channel1:
    fmt.Println("received", msg1)
  case msg2 := <-channel2:
    fmt.Println("received", msg2)
  }
}
```

如果没有收到消息，可使用超时时间，这让select语句在指定时间后不再阻塞，以便接着往下执行。

```go
select{
  case msg1 := <-channel1:
    fmt.Println("received", msg1)
  case msg2 := <-channel2:
    fmt.Println("received", msg2)
  case <-time.After(500*time.Millisecond):
    fmt.Println("no messages received.giving up.")
  }
```

**退出通道**
在已知需要停止执行的时间的情况下，使用超时时间是不错的选择，但在有些情况下，不确定select语句何时返回，因此不能使用定时器,这种情况下可使用退出通道。这种技术并非语言规范的组成部分，但可通过向通道发送消息来理解退出阻塞的select语句。

程序需要使用select语句实现无限制地阻塞，但同时要求能够随时返回。可在语句中添加一个退出通道，可向退出通道发送消息来结束语句，从而停止阻塞。可将其视为开关，其命名随意，通常为stop或quit。


```go
//stop or quit
func sender(c chan string) {
  t := time.NewTicker(1 * time.Second)
  for {
    c <- "I'm sending a message"
    <-t.C
  }
}
func main() {
  messages := make(chan string)
  stop := make(chan bool)
  go sender(messages)
  go func() {
    time.Sleep(time.Second * 2)
    fmt.Println("Time's up!")
    stop <- true
  }()
  for {
    select {
    case <-stop:
      return
    case msg := <-messages:
      fmt.Println(msg)
    }
  }
}
```


关闭缓冲通道意味者不能再向它发送消息。缓冲的消息会被保留，可供接收者读取。










