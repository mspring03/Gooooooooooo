# **Switch 문**
여러 값을 비교해야 하는 경우 혹은 다수의 조건식을 체크해야 하는 경우 **switch** 문을 사용한다. 

다른 언어들과 비슷하게 **switch** 문 뒤에 하나의 변수(혹은 **Expression**)을 지정하고, **case** 문에 해당 변수가 가질 수 있는 값들을 저정하여, 각 블럭들을 실행한다. 
``` go
var name string
var category = 1

switch category {
case 1:
    name = "Paper Book"
case 2:
    name = "eBook"
case 3, 4:
    name = "Blog"
default:
    name = "Other"
}
println(name)
    
// Expression을 사용한 경우
switch x := category << 2; x - 1 {
    //...
}   
```

**Go**의 **switch** 문에서 한가지 특징적인 용법은 **switch** 뒤에 조건변후 혹은 **Expression**을 적지 않는 용법이다. 

이 경우 **case** 조건문들을 순서대로 검사하여 조건에 맞는경우 **case** 블럭을 실행하고 **switch** 문을 빠져나온다.
``` go
func grade(score int) {
    switch {
    case score >= 90:
        println("A")
    case score >= 80:
        println("B")
    case score >= 70:
        println("C")
    case score >= 60:
        println("D")
    default:
        println("No Hope")
    }
}   

```

**Go**의 또 다른 용법은 **switch** 변수의 타입을 검사하는 타입 **switch**가 있다.
``` go
switch v.(type) {
case int:
    println("int")
case bool:
    println("bool")
case string:
    println("string")
default:
    println("unknown")
}   
```

**Go** 언어는 컴파일러가 **case** 문 마지막에 **break** 문을 생략하면 자동으로 추가해준다.  

만약 **break**를 무시하고 싶으면 **fallthrough** 문을 명시해주면 된다.
``` go
package main
 
import "fmt"
 
func main() {
    check(2)
}
 
func check(val int) {
    switch val {
    case 1:
        fmt.Println("1 이하")
        fallthrough
    case 2:
        fmt.Println("2 이하")
        fallthrough
    case 3:
        fmt.Println("3 이하")
        fallthrough
    default:
        fmt.Println("default 도달")
    }
}
```