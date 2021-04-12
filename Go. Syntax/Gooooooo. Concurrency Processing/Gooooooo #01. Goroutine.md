# **Go루틴**
**Go루틴**은 **Go 런타임**이 관리하는 **Lightweight 논리적 쓰레드**이다.
* **Go**에서 **"go"키워드**를 사용하여 함수를 호출하면, 런타임시 새로운 **goroutine**을 실행한다.
* **goroutine**은 비동기적으로 함수 루틴을 실행하므로, 여러 코드를 동시에 실행하는데 사용된다.
* **goroutine**은 OS 쓰레드보다 훨신 가볍게 비동기 처리를 구현하기 위해 만들 것으로, 기본적으로 Go 런타임이 자체 관리한다. 

**Go 런타임** 상에서 관리되는 작업단위인 여러 **goroutine**들은 종종 하나의 OS 쓰레드 1개로도 실행되곤 한다. 

즉, **Go루틴**들은 OS 쓰레드와 1대 1로 대응되지 않고, **Multiplexting**으로 훨식 적은 OS 쓰레드를 사용한다

**Go 런타임**은 **Go루틴**을 관리하면서 **Go 채널**을 통해 **Go루틴**간의 통신을 쉽게 할 수 있도록 하였다.

### **코드**
``` go
package main
 
import (
    "fmt"
    "time"
)
 
func say(s string) {
    for i := 0; i < 10; i++ {
        fmt.Println(s, "***", i)
    }
}
 
func main() {
    // 함수를 동기적으로 실행
    say("Sync")
 
    // 함수를 비동기적으로 실행
    go say("Async1")
    go say("Async2")
    go say("Async3")
 
    // 3초 대기
    time.Sleep(time.Second * 3)
}
```

## **익명함수 Go루틴**
**Go루틴**은 익명함수에 대해 사용할 수도 있다. 

즉, **Go** 키워드 뒤에 익명함수를 바로 정의하는 것으로, 이는 **익명함수를 비동기로 실행**하게 한다.
``` go
package main
 
import (
    "fmt"
    "sync"
)
 
func main() {
    // WaitGroup 생성. 2개의 Go루틴을 기다림.
    var wait sync.WaitGroup
    wait.Add(2)
 
    // 익명함수를 사용한 goroutine
    go func() {
        defer wait.Done() //끝나면 .Done() 호출
        fmt.Println("Hello")
    }()
 
    // 익명함수에 파라미터 전달
    go func(msg string) {
        defer wait.Done() //끝나면 .Done() 호출
        fmt.Println(msg)
    }("Hi")
 
    wait.Wait() //Go루틴 모두 끝날 때까지 대기
}
```

여기서 **sync.WaitGroup**을 사용하고 있는데, 이는 기본적으로 여러 Go루틴들이 끝날 때까지 기다리는 역할을 한다.

## **다중 CPU처리**
Go는 디폴트로 1개의 CPU를 사용한다. 즉, 여러개의 Go 루틴을 만들더라도, 1개의 CPU에서 작업을 시분할하여 처리한다. 

만약 머신이 복수개의 CPU를 가진 경우, Go프로그램을 다중 CPU에서 병렬처리 하게 할 수 있는데,  병렬처리를 위해서는 **runtime.GOMAXPROCS(CPU수)** 함수를 호출하여야 한다.

### **코드**
``` go
package main
 
import (
    "runtime"  
)
 
func main() {
    // 4개의 CPU 사용
    runtime.GOMAXPROCS(4)
 
    //...
}
```

**동시성**및 **병렬성**과 비슷하게 들리지만, 전혀 다른 개념이다. 

아래는 이 둘을 구분하기 위해 **golang.org** 블로그에 소개된 글이다. 
> In programming, concurrency is the composition of independently executing processes, while parallelism is the simultaneous execution of (possibly related) computations. Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.