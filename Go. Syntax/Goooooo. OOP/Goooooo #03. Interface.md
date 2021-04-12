# **인터페이스**
> 구조체가 필드들의 집합체라면 interface는 메서드들의 집합체이다.

## **인터페이스 선언**
``` go
type Shape interface {
    area() float64
    perimeter() float64
}
```

## **인터페이스 사용**
인터페이스를 사용하는 예로 함수가 파라미터로 인터페이스를 받아들이는 경우를 들 수 있다. 

함수 파라미터가 interface인 경우, 이는 어떤 타입이든 해당 인터페이스를 구현하기만 하면 모두 입력 파라미터로 사용될 수 있다는 것을 의미한다.

### **코드**
//섹스가 나는 좋아
``` go
func main() {
    r := Rect{10., 20.}
    c := Circle{10}
 
    showArea(r, c)
}
 
func showArea(shapes ...Shape) {
    for _, s := range shapes {
        a := s.area() //인터페이스 메서드 호출
        println(a)
    }
}
```

## **인터페이스 타입**
빈 인터페이스를 타입으로 두면 아무 타입이나 담을 수 있는 컨테이너가 된다.

즉 다른 언어에서 흔히 일컫는 동적 타입이라고 볼 수 있다.

### **코드**
``` go
package main

import "fmt"
 
func main() {
    var x interface{}
    x = 1 
    x = "Tom"
 
    printIt(x)
}
 
func printIt(v interface{}) {
    fmt.Println(v) //Tom
}
```

## **Type Assertion**
Interface type의 x와 타입 T에 대하여 x.(T)로 표현했을 때, 이는 x가 nil이 아니며, x는 T 타입에 속한다는 점을 확인하는 것으로 이러한 표현을 Type Assertion이라고 부른다.

``` go
func main() {
    var a interface{} = 1
 
    i := a       // a와 i 는 dynamic type, 값은 1
    j := a.(int) // j는 int 타입, 값은 1
 
    println(i)  // 포인터주소 출력
    println(j)  // 1 출력
}
```