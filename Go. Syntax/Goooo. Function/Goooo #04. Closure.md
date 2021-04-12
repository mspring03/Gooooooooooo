# **클로저**
Go 언어에서 함수는 클로저로 사용될 수도 있다. 

클로저는 함수 바깥에 있는 변수를 참조하는 함수 값을 일컫는데, 이때의 함수는 바깥 변수를 마치 함수 안으로 끌어들인듯이 그 변수를 읽거나 쓸 수 있게 된다.

### 코드
```go
package main
 
func nextValue() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}
 
func main() {
    next := nextValue()
 
    println(next())  // 1
    println(next())  // 2
    println(next())  // 3
 
    anotherNext := nextValue()
    println(anotherNext()) // 1 다시 시작
    println(anotherNext()) // 2
}
```