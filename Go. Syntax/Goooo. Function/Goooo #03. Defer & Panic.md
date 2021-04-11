# **Defer & Panic**
## **지연 실행 Defer**
Go의 **defer** 키워드는 특정 문장 혹은 함수를 나중에 실행하게 한다. 

일반적으로 **defer**은 finally 블럭처럼 마지막에 **Clean-up** 작업을 워해 사용된다.

이는 차후 함수에서 어떤 에러가 발생하더라도 항상 파일을 **Close**할 수 있도록 한다. 

### **코드** 
``` go
package main
 
import "os"
 
func main() {
    f, err := os.Open("1.txt")
    if err != nil {
        panic(err)
    }
 
    // main 마지막에 파일 close 실행
    defer f.Close()
 
    // 파일 읽기
    bytes := make([]byte, 1024)
    f.Read(bytes)
    println(len(bytes))
}
```

## **Panic 함수**
**Go** 내장함수인 **panic()** 함수는 현재 함수를 즉시 멈추고 현재 함수에 **defer** 함수들을 모두 실행한 후 즉시 리턴한다.  

이러한 **panic**의 실행 방식은 상위함수에도 똑같이 적용되고, 계속 콜스택을 타고 올라가며 적용된다. 

마지막에는 프로그램이 에러를 내고 종료된다.

### **코드**
``` go
package main
 
import "os"
 
func main() {
    // 잘못된 파일명을 넣음
    openFile("Invalid.txt")
     
    // openFile() 안에서 panic이 실행되면
    // 아래 println 문장은 실행 안됨
    println("Done") 
}
 
func openFile(fn string) {
    f, err := os.Open(fn)
    if err != nil {
        panic(err)
    }
 
    defer f.Close()
}
```

## **Recover 함수**
**Go** 내장함수인 **recover()**함수는 **panic**함수에 의한 패닉상태를 정상으로 되돌리는 함수이다.

위에 코드에서는 **main**함수에서 **println()**이 호출되지 못하고 프로그램이 다운되지만 **recover** 함수를 이용하면 **panic** 상태를 제거하여 프로그램을 계속 진행한다.

### **코드**
``` go
package main
 
import (
    "fmt"
    "os"
)
 
func main() {
    // 잘못된 파일명을 넣음
    openFile("Invalid.txt")
 
    // recover에 의해
    // 이 문장 실행됨
    println("Done") 
}
 
func openFile(fn string) {
    // defer 함수. panic 호출시 실행됨
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("OPEN ERROR", r)
        }
    }()
 
    f, err := os.Open(fn)
    if err != nil {
        panic(err)
    }
 
    defer f.Close()
}
```