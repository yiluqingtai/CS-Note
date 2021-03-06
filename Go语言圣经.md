书籍地址：[前言 · Go语言圣经 (itsfun.top)](https://book.itsfun.top/gopl-zh/)

## 前言

### Go语言项目

1、Go语言拥有自动垃圾回收、一个包系统、函数作为一等公民、词法作用域、系统调用接口、只读的UTF8字符串等。

2、Go语言没有隐式的数值转换，没有构造函数和析构函数，没有运算符重载，没有默认参数，也没有继承，没有泛型，没有异常，没有宏，没有函数修饰，更没有线程局部存储。

3、Go语言有足够的类型系统以避免动态语言中那些粗心的类型错误，但是，Go语言的类型系统相比传统的强类型语言又要简洁很多。

4、Go语言提供了基于CSP的并发特性支持。Go语言的动态栈使得轻量级线程goroutine的初始栈可以很小，因此，创建一个goroutine的代价很小，创建百万级的goroutine完全是可行的。

5、Go语言的标准库（通常被称为语言自带的电池），提供了清晰的构建模块和公共接口，包含I/O操作、文本处理、图像、密码学、网络和分布式应用程序等，并支持许多标准化的文件格式和编解码协议。

### 本书的组织

1、第一章到第五章是基础部分，主流命令式编程语言这部分都类似。

个别之处，Go语言有自己特色的语法和风格，但是大多数程序员能很快适应。

其余章节是Go语言特有的：方法、接口、并发、包、测试和反射等语言特性。

2、Go语言的面向对象机制与一般语言不同。它没有类层次结构，甚至可以说没有类；仅仅通过组合（而不是继承）简单的对象来构建复杂的对象。

方法不仅可以定义在结构体上，而且，可以定义在任何用户自定义的类型上；并且，具体类型和抽象类型（接口）之间的关系是隐式的，所以很多类型的设计者可能并不知道该类型到底实现了哪些接口。

3、其他资料

Go语言安装：[Download and install - The Go Programming Language (golang.org)](https://golang.org/doc/install)。（linux下流程：下载压缩包、解压、设置环境变量）

Go语言的官方博客 https://blog.golang.org 会不定期发布一些Go语言最好的实践文章，包括当前语言的发展状态、未来的计划、会议报告和Go语言相关的各种会议的主题等信息。

在线访问的一个有价值的地方是可以从web页面运行Go语言的程序（而纸质书则没有这么便利了）。这个功能由来自 https://play.golang.org 的 Go Playground 提供。

Go语言是一个开源项目，你可以在 https://golang.org/pkg 阅读标准库中任意函数和类型的实现代码，和下载安装包的代码完全一致。

### 更多的信息

## 1 入门

### 1.1 Hello,World

1、Go是一门编译型语言，Go语言的工具链将源代码及其依赖转换成计算机的机器指令（译注：静态编译）。

2、Go语言提供的工具都通过一个单独的命令go调用，go命令有一系列子命令。最简单的一个子命令就是run。这个命令编译一个或多个以.go结尾的源文件，链接库文件，并运行最终生成的可执行文件。

3、go build命令编译生成可执行文件。

4、go get命令从网上下载代码，需要提前设置好GOPATH变量。

5、go语言的helloworld

```go
package main

import 'fmt'

func main() {
    fmt.Println("hello, world!")
}
```

6、Go语言的代码通过包（package）组织，包类似于其它语言里的库（libraries）或者模块（modules）。

一个包由位于单个目录下的一个或多个.go源代码文件组成，目录定义包的作用。

每个源文件都以一条package声明语句开始，helloworld的例子里就是package main，表示该文件属于哪个包，紧跟着一系列导入（import）的包，之后是存储在这个文件里的程序语句。

Go的标准库提供了100多个包，以支持常见功能，如输入、输出、排序以及文本处理。比如fmt包，就含有格式化输出、接收输入的函数。Println是其中一个基础函数，可以打印以空格间隔的一个或多个值，并在最后添加一个换行符，从而输出一整行。

main包比较特殊。它定义了一个独立可执行的程序，而不是一个库。在main里的main 函数 也很特殊，它是整个程序执行时的入口。

必须恰当导入需要的包，缺少了必要的包或者导入了不需要的包，程序都无法编译通过。

7、包声明之后是组成程序的函数、变量、常量、类型的声明语句（分别由关键字func、var、const、type定义）。

8、Go语言不需要在语句或者声明的末尾添加分号，除非一行上有多条语句。

9、gofmt工具把代码格式化为标准格式，需要养成格式化代码的好习惯。

### 1.2 命令行参数

1、os包以跨平台的方式，提供了一些与操作系统交互的函数和变量。程序的命令行参数可从os包的Args变量获取；os包外部使用os.Args访问该变量。

2、os.Args变量是一个字符串（string）的切片（slice）。

3、os.Args的第一个元素：os.Args[0]，是命令本身的名字；其它的元素则是程序启动时传给它的参数。

4、echo例子：打印命令行参数。

5、变量会在声明时直接初始化。如果变量没有显式初始化，则被隐式地赋予其类型的零值（zero value），数值类型是0，字符串类型是空字符串""。

6、对string类型，+运算符连接字符串。

7、Go语言只有for循环这一种循环语句。

for循环三个部分不需括号包围。大括号强制要求，左大括号必须和post语句在同一行。

initialization语句是可选的，在循环开始前执行。initalization如果存在，必须是一条简单语句（simple statement），即，短变量声明、自增语句、赋值语句或函数调用。

for循环的这三个部分每个都可以省略，如果省略initialization和post，分号也可以省略。

8、另一种for循环

在某种数据类型的区间（range）上遍历，如字符串或切片。使用range关键词。

每次循环迭代，range产生一对值；索引以及在该索引处的元素值。

不需要索引，可以使用空标识符（blank identifier），即_（也就是下划线）。空标识符可用于在任何语法需要变量名但程序逻辑不需要的时候（如：在循环里）丢弃不需要的循环索引，并保留元素值。

9、声明一个变量有好几种方式

```go
s := "" // 是一条短变量声明，最简洁，但只能用在函数内部，而不能用于包变量
var s string // 依赖于字符串的默认初始化零值机制，被初始化为""
var s = "" // 用得很少，除非同时声明多个变量。
var s string = "" // 显式地标明变量的类型，当变量类型与初值类型相同时，类型冗余，但如果两者类型不同，变量类型就必须了
//实践中一般使用前两种形式中的某个，初始值重要的话就显式地指定变量的类型，否则使用隐式初始化。
```

### 1.3 查找重复的行

1、正如for循环一样，if语句条件两边也不加括号，但是主体部分需要加。if语句的else部分是可选的，在if的条件为false时执行。

2、内置函数make创建空map。例如：`make(map[string]int)`，键为字符串，值为int。

3、bufio包处理输入和输出方便又高效。Scanner类型是该包最有用的特性之一，它读取输入并将其拆成行或单词；通常是处理行形式的输入最简单的方法。

4、类似于C或其它语言里的printf函数，fmt.Printf函数对一些表达式产生格式化输出。

5、Go读取文件：os.Open函数。os.Open函数返回两个值。第一个值是被打开的文件(*os.File），其后被Scanner读取。os.Open返回的第二个值是内置error类型的值。如果err等于内置值nil（译注：相当于其它语言里的NULL），那么文件被成功打开。

6、错误处理：使用Fprintf与表示任意类型默认格式值的动词%v，向标准错误流打印一条信息，然后dup继续处理下一个文件。

7、函数和包级别的变量（package-level entities）可以任意顺序声明，并不影响其被调用。

8、Go中的函数参数传递默认相当于C++中的引用传递。

9、ReadFile函数（来自于io/ioutil包），读取指定文件的全部内容。

10、strings.Split函数把字符串分割成子串的切片。

## 2 程序结构

### 2.1 命名

1、一个名字必须以一个字母（Unicode字母）或下划线开头，后面可以跟任意数量的字母、数字或下划线。大写字母和小写字母是不同的：heapSort和Heapsort是两个不同的名字。

2、有大约30多个预定义的名字，比如int和true等，主要对应内建的常量、类型和函数。这些内部预先定义的名字并不是关键字，你可以在定义中重新使用它们。在一些特殊的场景中重新定义它们也是有意义的，但是也要注意避免过度而引起语义混乱。

3、名字的开头字母的大小写决定了名字在包外的可见性。如果一个名字是大写字母开头的（译注：必须是在函数外部定义的包级名字；包级函数名本身也是包级名字），那么它将是导出的，也就是说可以被外部的包访问，例如fmt包的Printf函数就是导出的，可以在fmt包外部访问。包本身的名字一般总是用小写字母。

4、在习惯上，Go语言程序员推荐使用 驼峰式 命名，当名字由几个单词组成时优先使用大小写分隔，而不是优先用下划线分隔。

### 2.2 声明

1、声明语句定义了程序的各种实体对象以及部分或全部的属性。

2、Go语言主要有四种类型的声明语句：var、const、type和func，分别对应变量、常量、类型和函数实体对象的声明。

3、每个源文件中以包的声明语句开始，说明该源文件是属于哪个包。

包声明语句之后是import语句导入依赖的其它包。

然后是包一级的类型、变量、常量、函数的声明语句。

4、在包一级声明语句声明的名字可在整个包对应的每个源文件中访问，而不是仅仅在其声明语句所在的源文件中访问。相比之下，局部声明的名字就只能在函数内部很小的范围被访问。

5、一个函数的声明由一个函数名字、参数列表（由函数的调用者提供参数变量的具体值）、一个可选的返回值列表和包含函数定义的函数体组成。

### 2.3 变量

1、变量声明的一般语法如下：`var 变量名字 类型 = 表达式`

其中“类型”或“= 表达式”两个部分可以省略其中的一个。如果省略的是类型信息，那么将根据初始化表达式来推导变量的类型信息。

如果初始化表达式被省略，那么将用零值初始化该变量。 

2、零值初始化机制可以确保每个声明的变量总是有一个良好定义的值，因此在Go语言中不存在未初始化的变量。

Go语言程序员应该让一些聚合类型的零值也具有意义，这样可以保证不管任何类型的变量总是有一个合理有效的零值状态。

3、也可以在一个声明语句中同时声明一组变量，或用一组初始化表达式声明并初始化一组变量。如果省略每个变量的类型，将可以声明多个类型不同的变量（类型由初始化表达式推导）

4、一组变量也可以通过调用一个函数，由函数返回的多个返回值初始化。

**2.3.1 简短变量声明**

1、在函数内部，有一种称为简短变量声明语句的形式可用于声明和初始化局部变量。它以“名字 := 表达式”形式声明变量，变量的类型根据表达式来自动推导。

因为简洁和灵活的特点，简短变量声明被广泛用于大部分的局部变量的声明和初始化。var形式的声明语句往往是用于需要显式指定变量类型的地方，或者因为变量稍后会被重新赋值而初始值无关紧要的地方。

请记住“:=”是一个变量声明语句，而“=”是一个变量赋值操作。

2、简短变量声明语句也可以用来声明和初始化一组变量。

简短变量声明左边的变量可能并不是全部都是刚刚声明的。如果有一些已经在相同的词法域声明过了（§2.7），那么简短变量声明语句对这些已经声明过的变量就只有赋值行为了。

但简短变量声明语句中必须至少要声明一个新的变量。

**2.3.2 指针**

1、并不是每一个值都会有一个内存地址，但是对于每一个变量必然有对应的内存地址。

通过指针，我们可以直接读或更新对应变量的值，而不需要知道该变量的名字（如果变量有名字的话）。

指针的定义和C差不多。

2、任何类型的指针的零值都是nil。

3、在Go语言中，返回函数中局部变量的地址也是安全的。

4、如果将指针作为参数调用函数，那将可以在函数中通过该指针来更新变量的值。

5、指针是实现标准库中flag包的关键技术，它使用命令行参数来设置对应变量的值，而这些对应命令行标志参数的变量可能会零散分布在整个程序中。

**2.3.3 new函数**

1、另一个创建变量的方法是调用内建的new函数。

表达式new(T)将创建一个T类型的匿名变量，初始化为T类型的零值，然后返回变量地址，返回的指针类型为*T。

2、用new创建变量和普通变量声明语句方式创建变量没有什么区别，除了不需要声明一个临时变量的名字外，我们还可以在表达式中使用new(T)。

new函数类似是一种语法糖，而不是一个新的基础概念。

3、new函数使用通常相对比较少，因为对于结构体来说，直接用字面量语法创建新变量的方法会更灵活。

**2.3.4 变量的生命周期**

1、对于在包一级声明的变量来说，它们的生命周期和整个程序的运行周期是一致的。

2、局部变量的生命周期则是动态的：每次从创建一个新变量的声明语句开始，直到该变量不再被引用为止，然后变量的存储空间可能被回收。函数的参数变量和返回值变量都是局部变量。它们在函数每次被调用的时候创建。

3、函数的右小括弧也可以另起一行缩进，同时为了防止编译器在行尾自动插入分号而导致的编译错误，可以在末尾的参数变量后面显式插入逗号。

4、Go的自动垃圾回收器：从每个包级的变量和每个当前运行函数的每一个局部变量开始，通过指针或引用的访问路径遍历，是否可以找到该变量。如果不存在这样的访问路径，那么说明该变量是不可达的，也就是说它是否存在并不会影响程序后续的计算结果。

因为一个变量的有效周期只取决于是否可达，因此一个循环迭代内部的局部变量的生命周期可能超出其局部作用域。同时，局部变量可能在函数返回之后依然存在。

5、编译器会自动选择在栈上还是在堆上分配局部变量的存储空间，但可能令人惊讶的是，这个选择并不是由用var还是new声明变量的方式决定的。

在任何时候，你并不需为了编写正确的代码而要考虑变量的逃逸行为，要记住的是，逃逸的变量需要额外分配内存，同时对性能的优化可能会产生细微的影响。

6、Go语言的自动垃圾收集器对编写正确的代码是一个巨大的帮助。

如果将指向短生命周期对象的指针保存到具有长生命周期的对象中，特别是保存到全局变量时，会阻止对短生命周期对象的垃圾回收（从而可能影响程序的性能）。

### 2.4 赋值

1、自增和自减是语句，而不是表达式，因此`x = i++`之类的表达式是错误的。

**2.4.1 元组赋值**

1、元组赋值是另一种形式的赋值语句，它允许同时更新多个变量的值。在赋值之前，赋值语句右边的所有表达式将会先进行求值，然后再统一更新左边对应变量的值。

在交换值的时候很有用。

2、如果表达式太复杂的话，应该尽量避免过度使用元组赋值；因为每个变量单独赋值语句的写法可读性会更好。

但元组赋值在某些情况很简洁。

3、可以使用有多个返回值的函数进行元组赋值。通常，这类函数会用额外的返回值来表达某种错误类型。

这种错误类型可能是error类型，也可能是布尔值。

4、map查找、类型断言或通道接（§8.4.2）出现在赋值语句的右边时，并不一定是产生两个结果，也可能只产生一个结果。对于只产生一个结果的情形，map查找失败时会返回零值，类型断言失败时会发生运行时panic异常，通道接收失败时会返回零值（阻塞不算是失败）。

**2.4.2 可赋值性**

1、隐式赋值：函数调用会隐式地将调用参数的值赋值给函数的参数变量，一个返回语句会隐式地将返回操作的值赋值给结果变量，一个复合类型的字面量也会产生赋值行为。

2、可赋值性：类型必须完全匹配，nil可以赋值给任何指针或引用类型的变量。常量则有更灵活的赋值规则，因为这样可以避免不必要的显式的类型转换。

### 2.5 类型

1、一个类型声明语句创建了一个新的类型名称，和现有类型具有相同的底层结构。新命名的类型提供了一个方法，用来分隔不同概念的类型，这样即使它们底层类型相同也是不兼容的。

2、声明一个新类型的方法：`type 类型名字 底层类型`。、

3、类型声明语句一般出现在包一级，因此如果新创建的类型名字的首字符大写，则在包外部也可以使用。

4、刻意区分类型，可以避免一些像无意中使用不同单位的底层类型混合计算导致的错误。

5、对于每一个类型T，都有一个对应的类型转换操作T(x)，用于将x转为T类型（译注：如果T是指针类型，可能会需要用小括弧包装T，比如`(*int)(0)`）。

只有当两个类型的底层基础类型相同时，才允许这种转型操作，或者是两者都是指向相同底层结构的指针类型，这些转换只改变类型而不会影响值本身。

6、数值类型之间的转型也是允许的，这类转换可能改变值的表现。在任何情况下，运行时不会发生转换失败的错误（译注: 错误只会发生在编译阶段）。

7、一个命名的类型可以提供书写方便，特别是可以避免一遍又一遍地书写复杂类型。

8、命名类型还可以为该类型的值定义新的行为。这些行为表示为一组关联到该类型的函数集合，我们称为类型的方法集。

许多类型都会定义一个String方法，因为当使用fmt包的打印方法时，将会优先使用该类型对应的String方法返回的结果打印。

### 2.6 包和文件

1、Go语言中的包和其他语言的库或模块的概念类似，目的都是为了支持模块化、封装、单独编译和代码重用。

2、通常一个包所在目录路径的后缀是包的导入路径。

3、每个包都对应一个独立的名字空间。

4、包还可以让我们通过控制哪些名字是外部可见的来隐藏内部实现信息。

如果一个名字是大写字母开头的，那么该名字是导出的（译注：因为汉字不区分大小写，因此汉字开头的名字是没有导出的）。

5、包级别的名字，例如在一个文件声明的类型和常量，在同一个包的其他源文件也是可以直接访问的，就好像所有代码都在一个文件一样。

6、每个源文件的包声明前紧跟着的注释是包注释。

通常，包注释的第一句应该先是包的功能概要说明。一个包通常只有一个源文件有包注释。

如果包注释很大，通常会放到一个独立的doc.go文件中。

**2.6.1 导入包**

1、在Go语言程序中，每个包都有一个全局唯一的导入路径。

这些字符串的具体含义是由构建工具来解释的。当使用Go语言自带的go工具箱时，一个导入路径代表一个目录中的一个或多个Go源文件。

2、除了包的导入路径，每个包还有一个包名，包名一般是短小的名字（并不要求包名是唯一的），包名在包的声明处指定。

按照惯例，一个包的名字和包的导入路径的最后一个字段相同。

3、导入语句将导入的包绑定到一个短小的名字，然后通过该短小的名字就可以引用包中导出的全部内容。

在默认情况下，导入的包绑定到包声明语句指定的名字，但是我们也可以绑定到另一个名称，以避免名字冲突。

4、如果导入了一个包，但是又没有使用该包将被当作一个编译错误处理。

5、我们可以使用golang.org/x/tools/cmd/goimports导入工具，它可以根据需要自动添加或删除导入的包；

许多编辑器都可以集成goimports工具，然后在保存文件的时候自动运行。类似的还有gofmt工具，可以用来格式化Go源文件。

**2.6.2 包的初始化**

1、包的初始化首先是解决包级变量的依赖顺序，然后按照包级变量声明出现的顺序依次初始化。

2、如果包中含有多个.go源文件，它们将按照发给编译器的顺序进行初始化，Go语言的构建工具首先会将.go文件根据文件名排序，然后依次调用编译器编译。

3、对于在包级别声明的变量，如果有初始化表达式则用表达式初始化，没有初始化表达式的可以用一个特殊的init初始化函数来简化初始化工作。每个文件都可以包含多个init初始化函数。

init初始化函数除了不能被调用或引用外，其他行为和普通函数类似。在每个文件中的init初始化函数，在程序开始执行时按照它们声明的顺序被自动调用。

对于需要复杂处理的变量初始化，可以通过将初始化逻辑包装为一个匿名函数处理。

4、每个包在解决依赖的前提下，以导入声明的顺序初始化，每个包只会被初始化一次。因此，如果一个p包导入了q包，那么在p包初始化的时候可以认为q包必然已经初始化过了。

### 2.7 作用域

1、声明语句的作用域对应的是一个源代码的文本区域；它是一个编译时的属性。一个变量的生命周期是指程序运行时变量存在的有效时间段，在此时间区域内它可以被程序的其他部分引用；是一个运行时的概念。

2、导入的包是对应源文件级的作用域，因此只能在当前的文件中访问导入的fmt包，当前包的其它源文件无法访问在当前源文件导入的包。

3、Go语言的习惯是在if中处理错误然后直接返回，这样可以确保正常执行的语句不需要代码缩进。

## 3 基本数据类型

1、Go语言将数据类型分为四类：基础类型、复合类型、引用类型和接口类型。

2、基础类型包括：数字、字符串和布尔型。

3、复合数据类型包括数组和结构体——是通过组合简单类型，来表达更加复杂的数据结构。

4、引用类型包括指针、切片、字典、函数、通道，虽然数据种类很多，但它们都是对程序中一个变量或状态的间接引用。

### 3.1 整型

1、Go语言同时提供了有符号和无符号类型的整数运算。这里有int8、int16、int32和int64四种截然不同大小的有符号整数类型，分别对应8、16、32、64bit大小的有符号整数，与此对应的是uint8、uint16、uint32和uint64四种无符号整数类型。

2、两种一般对应特定CPU平台机器字大小的有符号和无符号整数int和uint，不同的平台上会有不同的大小。

3、无符号的整数类型uintptr，没有指定具体的bit大小但是足以容纳指针。uintptr类型只有在底层编程时才需要，特别是Go语言和C语言函数库或操作系统接口相交互的地方。

4、Printf函数的%b参数打印二进制格式的数字；其中%08b中08表示打印至少8个字符宽度，不足的前缀部分用0填充。

5、即使数值本身不可能出现负数，我们还是倾向于使用有符号的int类型。无符号数往往只有在位运算或其它特殊的运算场景才会使用，就像bit集合、分析二进制文件格式或者是哈希和加密操作等。它们通常并不用于仅仅是表达非负数量的场合。

6、对于每种类型T，如果转换允许的话，类型转换操作T(x)将x转换为T类型。

7、当使用fmt包打印一个数值时，我们可以用%d、%o或%x参数控制输出的进制格式

%v打印默认格式，%d表示打印十进制整数，%s表示打印字符串，%c表示打印字符，%g表示打印浮点数。

通常Printf格式化字符串包含多个%参数时将会包含对应相同数量的额外操作数，但是%之后的[1]副词告诉Printf函数再次使用第一个操作数。

%后的#副词告诉Printf在用%o、%x或%X输出时生成0、0x或0X前缀。

8、字符使用%c参数打印，或者是用%q参数打印带单引号的字符。

### 3.2 浮点数

1、Go语言提供了两种精度的浮点数，float32和float64。

2、这些浮点数类型的取值范围可以从很微小到很巨大。浮点数的范围极限值可以在math包找到。

常量math.MaxFloat32表示float32能表示的最大数值，大约是 3.4e38；对应的math.MaxFloat64常量大约是1.8e308。

3、通常应该优先使用float64类型，因为float32类型的累计计算误差很容易扩散，并且float32能精确表示的正整数并不是很大。

很小或很大的数最好用科学计数法书写，通过e或E来指定指数部分。

4、math包中包含正无穷大+Inf和负无穷大-Inf，分别用于表示太大溢出的数字和除零的结果；还有NaN非数，一般用于表示无效的除法操作结果0/0或Sqrt(-1)。

函数math.IsNaN用于测试一个数是否是非数NaN，math.NaN则返回非数对应的值。虽然可以用math.NaN来表示一个非法的结果，但是测试一个结果是否是非数NaN则是充满风险的，因为NaN和任何数都是不相等的。



## 4 复合数据类型

1、复合数据类型：数组、slice、map和结构体。

2、数组和结构体是聚合类型；它们的值由许多元素或成员字段的值组成。数组是由同构的元素组成——每个数组元素都是完全相同的类型——结构体则是由异构的元素组成的。数组和结构体都是有固定内存大小的数据结构。

3、slice和map则是动态的数据结构，根据需要动态增长。

### 4.1 数组

1、因为数组的长度是固定的，因此在Go语言中很少直接使用数组。

2、和数组对应的类型是Slice（切片），它是可以增长和收缩的动态序列，slice功能也更灵活，但是要理解slice工作原理的话需要先理解数组。

3、默认情况下，数组的每个元素都被初始化为元素类型对应的零值，对于数字类型来说就是0。我们也可以使用数组字面值语法用一组值来初始化数组。

4、在数组字面值中，如果在数组的长度位置出现的是“...”省略号，则表示数组的长度是根据初始化值的个数来计算。

5、可以指定一个索引和对应值列表的方式初始化

```go
r := [...]int{99: -1} // 定义了一个100个元素的数组，只有最后一个元素为-1，其他的为0
```

6、Printf函数的%x副词参数指定以十六进制的格式打印数组或slice全部的元素，%t副词参数是用于打印布尔型数据，%T副词参数是用于显示一个值对应的数据类型。

7、当调用一个函数的时候，函数的每个调用参数将会被赋值给函数内部的参数变量，所以函数参数变量接收的是一个复制的副本，并不是原始调用的变量。

Go语言传入数组时一般显式地传入一个数组指针，那样的话函数通过指针对数组的任何修改都可以直接反馈到调用者。

### 4.2 Slice

1、Slice（切片）代表变长的序列，序列中每个元素都有相同的类型。一个slice类型一般写作[]T，其中T代表slice中元素的类型；slice的语法和数组很像，只是没有固定长度而已。

2、一个slice是一个轻量级的数据结构，提供了访问数组子序列（或者全部）元素的功能，而且slice的底层确实引用一个数组对象。

3、一个slice由三个部分构成：指针、长度和容量。

指针指向第一个slice元素对应的底层数组元素的地址，要注意的是slice的第一个元素并不一定就是数组的第一个元素。

长度对应slice中元素的数目；长度不能超过容量，容量一般是从slice的开始位置到底层数据的结尾位置。

内置的len和cap函数分别返回slice的长度和容量。

4、多个slice之间可以共享底层的数据，并且引用的数组部分区间可能重叠。

5、slice的切片操作s[i:j]，其中0 ≤ i≤ j≤ cap(s)，用于创建一个新的slice，引用s的从第i个元素开始到第j-1个元素的子序列。

新的slice将只有j-i个元素。如果i位置的索引被省略的话将使用0代替，如果j位置的索引被省略的话将使用len(s)代替。

如果切片操作超出cap(s)的上限将导致一个panic异常，但是超出len(s)则是意味着扩展了slice，因为新slice的长度会变大。

6、因为slice值包含指向第一个slice元素的指针，因此向函数传递slice将允许在函数内部修改底层数组的元素。

7、slice和数组的字面值语法很类似，它们都是用花括弧包含一系列的初始化元素，但是对于slice并没有指明序列的长度。这会隐式地创建一个合适大小的数组，然后slice的指针指向底层的数组。

和数组不同的是，slice之间不能比较，因此我们不能使用==操作符来判断两个slice是否含有全部相等元素。不过标准库提供了高度优化的bytes.Equal函数来判断两个字节型slice是否相等（[]byte），但是对于其他类型的slice，我们必须自己展开每个元素进行比较。

slice唯一合法的比较操作是和nil比较。一个nil值的slice并没有底层数组。一个nil值的slice的长度和容量都是0，但是也有非nil值的slice的长度和容量也是0的。

如果你需要测试一个slice是否是空的，使用len(s) == 0来判断，而不应该用s == nil来判断。

8、内置的make函数创建一个指定元素类型、长度和容量的slice。容量部分可以省略，在这种情况下，容量将等于长度。

**4.2.1 append函数**

1、内置的append函数用于向slice追加元素。

2、append添加元素时，如果底层数组容量不够，将会重新创建一个容量翻倍的数组并进行复制，然后添加。

3、通常将append返回的结果直接赋值给输入的slice变量。

4、内置的append函数则可以追加多个元素，甚至追加一个slice。

**4.2.2 Slice内存技巧**

1、一个slice可以用来模拟一个stack。

最初给定的空slice对应一个空的stack，然后可以使用append函数将新的值压入stack。

stack的顶部位置对应slice的最后一个元素。

通过收缩stack可以弹出栈顶的元素。

## 5 函数

### 5.1 函数声明

1、函数声明包括函数名、形式参数列表、返回值列表（可省略）以及函数体。

2、返回值列表描述了函数返回值的变量名以及类型。

3、如果一组形参或返回值有相同的类型，我们不必为每个形参都写出参数类型。

_符号可以强调某个参数未被使用。

Go语言没有默认参数值，也没有任何方法可以通过参数名指定形参，因此形参和返回值的变量名对于函数调用者而言没有意义。

4、你可能会偶尔遇到没有函数体的函数声明，这表示该函数不是以Go实现的。这样的声明定义了函数签名。

## 6 方法

1、Go语言使用方法来实现面向对象设计。

一个对象也就是一个简单的值或者一个变量，在这个对象中会包含一些方法，而一个方法则是一个一个和特殊类型关联的函数。一个面向对象的程序会用方法来表达其属性和对应的操作，这样使用这个对象的用户就不需要直接去操作对象，而是借助方法来做这些事情。

### 6.1 方法声明

1、在函数声明时，在其名字之前放上一个变量，即是一个方法。这个附加的参数会将该函数附加到这种类型上，即相当于为这种类型定义了一个独占的方法。

附加的参数叫做方法的接收器，早期的面向对象语言留下的遗产将调用一个方法称为“向一个对象发送消息”。

建议使用类型的第一个字母作为接收器。

## 7 接口

### 7.1 接口是合约

1、接口类型是一种抽象的类型。它不会暴露出它所代表的对象的内部值的结构和这个对象支持的基础操作的集合；它们只会表现出它们自己的方法。也就是说当你有看到一个接口类型的值时，你不知道它是什么，唯一知道的就是可以通过它的方法来做什么。

2、接口类型使用type ${name} interface 的形式定义，接口中提供了起约束作用的函数签名。

3、fmt包的Printf和Sprintf函数都使用了Fprintf函数来封装，Fprintf的第一个参数类型是一个接口io.Writer，约定了Writer函数签名，`*os.File`和`*bytes.Buffer`都实现了Writer函数签名，所以可以传递给Fprintf函数。

## 8 Goroutines和Channels

1、Go语言中的并发程序可以用两种手段来实现，Goroutines和Channels。

2、顺序通信进程CSP是一种现代的并发编程模型，在这种编程模型中值会在不同的运行实例（goroutine）中传递，尽管大多数情况下仍然是被限制在单一实例中。

### 8.1 Goroutines

1、在Go语言中，每一个并发的执行单元叫作一个goroutine。你可以简单地把goroutine类比作一个线程。

2、当一个程序启动时，其主函数即在一个单独的goroutine中运行，我们叫它main goroutine。

3、新的goroutine会用go语句来创建。

在语法上，go语句是一个普通的函数或方法调用前加上关键字go。

go语句会使其语句中的函数在一个新创建的goroutine中运行。

4、主函数返回时，所有的goroutine都会被直接打断，程序退出。

可以通过goroutine之间的通信来让一个goroutine请求其它的goroutine，并让被请求的goroutine自行结束执行。

## 9 基于共享变量的并发

### 9.1 竞争条件

1、如果在并发的情况下，这个函数可以正确地工作的话，那么我们就说这个函数是并发安全的，并发安全的函数不需要额外的同步工作。

2、我们可以把这个概念概括为一个特定类型的一些方法和操作函数，对于某个类型来说，如果其所有可访问的方法和操作都是并发安全的话，那么该类型便是并发安全的。

3、在一个程序中有非并发安全的类型的情况下，我们依然可以使这个程序并发安全。

4、只有当文档中明确地说明了其是并发安全的情况下，你才可以并发地去访问它。我们会避免并发访问大多数的类型，无论是将变量局限在单一的一个goroutine内，还是用互斥条件维持更高级别的不变性，都是为了这个目的。

5、包级别的导出函数一般情况下都是并发安全的。由于package级的变量没法被限制在单一的gorouine，所以修改这些变量“必须”使用互斥条件。

6、一个函数在并发调用时没法工作的原因太多了，比如死锁（deadlock）、活锁（livelock）和饿死（resource starvation）。

7、竞争条件指的是程序在多个goroutine交叉执行操作时，没有给出正确的结果。竞争条件是很恶劣的一种场景，因为这种问题会一直潜伏在你的程序里，然后在非常少见的时候蹦出来，或许只是会在很大的负载时才会发生，又或许是会在使用了某一个编译器、某一种平台或者某一种架构的时候才会出现。这些使得竞争条件带来的问题非常难以复现而且难以分析诊断。

8、数据竞争会在两个以上的goroutine并发访问相同的变量且至少其中一个为写操作时发生。

9、竞争条件的解决方法

第一种方法是不要去写变量。数据结构如果从不被修改或是不变量则是并发安全的，无需进行同步。

第二种避免数据竞争的方法是，避免从多个goroutine访问变量。由于其它的goroutine不能够直接访问变量，它们只能使用一个channel来发送请求给指定的goroutine来查询更新变量。这也就是不要使用共享数据来通信，使用通信来共享数据。如果流水线的每一个阶段都能够避免在将变量传送到下一阶段后再去访问它，那么对这个变量的所有访问就是线性的。其效果是变量会被绑定到流水线的一个阶段，传送完之后被绑定到下一个，以此类推。这种规则有时被称为串行绑定。

第三种避免数据竞争的方法是允许很多goroutine去访问变量，但是在同一个时刻最多只有一个goroutine在访问。这种方式被称为“互斥”。

## 10 包和工具

1、Go语言有超过100个的标准包，标准库为大多数的程序提供了必要的基础构件。

2、目前互联网上已经发布了非常多的Go语言开源包，它们可以通过 [http://godoc.org](https://godoc.org/) 检索。

3、Go还自带了工具箱，里面有很多用来简化工作区和包管理的小工具。

### 10.1 包简介

1、每个包一般都定义了一个不同的名字空间用于它内部的每个标识符的访问。每个名字空间关联到一个特定的包，让我们给类型、函数等选择简短明了的名字，这样可以在使用它们的时候减少和其它部分名字的冲突。

2、每个包还通过控制包内名字的可见性和是否导出来实现封装特性。通过限制包成员的可见性并隐藏包API的具体实现，将允许包的维护者在不影响外部包用户的前提下调整包的内部实现。通过限制包内变量的可见性，还可以强制用户通过某些特定函数来访问和更新内部变量，这样可以保证内部变量的一致性和并发时的互斥约束。

3、当我们修改了一个源文件，我们必须重新编译该源文件对应的包和所有依赖该包的其他包。即使是从头构建，Go语言编译器的编译速度也明显快于其它编译语言。

## 11 测试

1、控制软件复杂性的两种方法。

第一种是代码在被正式部署前需要进行代码评审。

第二种则是测试。

2、我们说测试的时候一般是指自动化测试，也就是写一些小的程序用来检测被测试代码（产品代码）的行为和预期的一样，这些通常都是精心设计的执行某些特定的功能或者是通过随机性的输入待验证边界的处理。

3、软件测试是一个巨大的领域。测试的任务可能已经占据了一些程序员的部分时间和另一些程序员的全部时间。对于每一种主流的编程语言，都会有一打的用于测试的软件包，同时也有大量的测试相关的理论，而且每种都吸引了大量技术先驱和追随者。

4、Go语言的测试技术是相对低级的。它依赖一个go test测试命令和一组按照约定方式编写的测试函数，测试命令可以运行这些测试函数。

5、在实践中，编写测试代码和编写程序本身并没有多大区别。我们编写的每一个函数也是针对每个具体的任务。我们必须小心处理边界条件，思考合适的数据结构，推断合适的输入应该产生什么样的结果输出。

### 11.1 go test

1、go test命令是一个按照一定的约定和组织来测试代码的程序。

2、在包目录内，所有以`_test.go`为后缀名的源文件在执行go build时不会被构建成包的一部分，它们是go test测试的一部分。

3、在`*_test.go`文件中，有三种类型的函数：测试函数、基准测试（benchmark）函数、示例函数。

一个测试函数是以Test为函数名前缀的函数，用于测试程序的一些逻辑行为是否正确。go test命令会调用这些测试函数并报告测试结果是PASS或FAIL。

基准测试函数是以Benchmark为函数名前缀的函数，它们用于衡量一些函数的性能；go test命令会多次运行基准测试函数以计算一个平均的执行时间。

示例函数是以Example为函数名前缀的函数，提供一个由编译器保证正确性的示例文档。

4、go test命令会遍历所有的`*_test.go`文件中符合上述命名规则的函数，生成一个临时的main包用于调用相应的测试函数，接着构建并运行、报告测试结果，最后清理测试中生成的临时文件。

## 12 反射

1、Go语言提供了一种机制，能够在运行时更新变量和检查它们的值、调用它们的方法和它们支持的内在操作，而不需要在编译时就知道这些变量的具体类型。这种机制被称为反射。

反射也可以让我们将类型本身作为第一类的值类型处理。

2、反射是一个复杂的内省技术，不应该随意使用，因此，尽管上面这些包内部都是用反射技术实现的，但是它们自己的API都没有公开反射相关的接口。

### 12.1 为何需要反射？

1、反射是用来检查未知类型的。



