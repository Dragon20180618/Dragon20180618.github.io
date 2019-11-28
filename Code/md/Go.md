# Gopher

***Study as a game***

## Go 的import

import 导入的都是文件夹，也就是说，如果你写了很多package在一个文件夹<br>

**像这样：**

directory : t1

> t2.go

```go
package mathClass
func Sub(x,y int)int{
	return x-y
}
```

> t3.go

```go
package mathClass
func Add(x,y int)int{
	return x+y
}
```

则导入t时可以将main函数所在的.go文件放到，与 文件夹 t 同级的目录

test.go

```go
package main

import (
	."fmt"
	"./t"
)

type rect struct {
	width  int
	height int
}

func main() {
	Println("Hello World")
	Println(sum(1,2))
	r :=rect{width:1,height:5}
	r.width=2
	Println(r.width)
	Println(mathClass.Add(1, 2))
	Println(mathClass.Sub(1, 2))
}
func sum(a int, b int) int {
	return (a + b)
}

```

其上的导入部分可变为

```go
import . "fmt"
import "./t"
```

但显然第一种方法要更简单。与此类似的，还有函数定义。如果一个函数需要两个类型一样的参数。可以这样书写。

```go
func test(a,b int)int{}
```

```go
func test(a,b int,c,d,float64)int{}
```

直接在最后写参数类型。

上述代码还包含了**结构体**

```go
type rect struct {
	width  int
	height int
}
```

实现一个rect对象的方法

```go
r :=rect{width:1,height:5}
```

其中的内容可以直接抽离，或者重新赋值

```go
r.width=2
Println(r.width)
```

