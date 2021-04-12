# **Go 채널**
**Go 채널**은 그 채널을 통하여 데이터를 주고 받는 통로라 볼 수 있는데, 채널은 **make()** 함수를 통해 미리 생성되어야 하며, 채널 연산자 <- 을 통해 데이터를 주고 받는다.

채널은 흔히 **goroutine**들 사이 데이타를 주고 받는데 사용되는데, 상대편이 준비될 때까지 채널에서 대기함으로써 별도의 **lock**을 걸지 않고 데이터를 동기화 하는데 사용된다.

### **코드**
``` go
package main
 
func main() {
  // 정수형 채널을 생성한다 
  ch := make(chan int)
 
  go func() {
    ch <- 123   //채널에 123을 보낸다
  }()
 
  var i int
  i = <- ch  // 채널로부터 123을 받는다
  println(i)
}
```

위 예제에서 메인 루틴은 마지막에서 채널로부터 데이타를 받고 있는데, 상대편 **goroutine**에서 데이타를 전송할 때까지는 계속 대기하게 된다. 

이를 이용하여 **Go루틴**이 끝날 때까지 기다리는 기능을 구현할 수 있다.

### **코드**
``` go
package main
 
import "fmt"
 
func main() {
    done := make(chan bool)
    go func() {
        for i := 0; i < 10; i++ {
            fmt.Println(i)
        }
        done <- true
    }()
 
    // 위의 Go루틴이 끝날 때까지 대기
    <-done
}
```

## **Go 채널 버퍼링**
채널을 함수의 파라미터로 전달할 때, 일반적으로 송수신을 모두 하는 채널을 전달하지만, 특별히 해당 채널로 송신만 할 것인지 혹은 수신만 할 것인지를 지정할 수도 있다.  

### **코드**
``` go
package main
 
import "fmt"
 
func main() {
    ch := make(chan string, 1)
    sendChan(ch)
    receiveChan(ch)
}
 
func sendChan(ch chan<- string) {
    ch <- "Data"
    // x := <-ch // 에러발생
}
 
func receiveChan(ch <-chan string) {
    data := <-ch
    fmt.Println(data)
}
```

## **채널 닫기**
채널을 오픈하고 데이터를 송신한 뒤에 **close()**함수를 사용하여 채널을 닫을 수 있다. 

채널을 닫게 되면, 해당 채널로는 더이상 송신을 할 수 없지만, 채널이 닫힌 이후에도 계속 수신은 가능하다.

### **코드**
``` go
package main
 
func main() {
    ch := make(chan int, 2)
     
    // 채널에 송신
    ch <- 1
    ch <- 2
     
    // 채널을 닫는다
    close(ch)
 
    // 채널 수신
    println(<-ch)
    println(<-ch)
     
    if _, success := <-ch; !success {
        println("더이상 데이타 없음.")
    }
}
```

## **채널 range 문**
채널에서 송신자가 송신을 한 후, 채널을 닫을 수 있다.

그리고 수신자는 임의의 갯수의 데이터를 채널이 닫힐 때까지 계속 수실할 수 있다. 

### **코드**
``` go
package main
 
func main() {
    ch := make(chan int, 2)
 
    // 채널에 송신
    ch <- 1
    ch <- 2
 
    // 채널을 닫는다
    close(ch)
 
    // 방법1
    // 채널이 닫힌 것을 감지할 때까지 계속 수신
    for {
        if i, success := <-ch; success {
            println(i)
        } else {
            break
        }
    }
 
    // 방법2
    // 위 표현과 동일한 채널 range 문
    for i := range ch {
        println(i)
    }
}
```

## **채널 select 문**
Go의 **select**문은 복수 채널들을 기다리면서 준비된 채널을 실행하는 기능을 제공한다.

즉, **select**문은 여러 개의 **case**문에서 각각 다른 채널을 기다리다가 준비가 된 채널 **case**를 실행하는 것이다. 
* 만약 복수 채널에 신호가 오면, Go 런타임이 랜덤하게 그 중 한개를 선택한다. 

하지만 **default**문이 있으면, case문 채널이 준비되지 않더라도 계속 대기하지 않고 바로 **default문**을 실행한다.

### **코드**
``` go
package main
 
import "time"
 
func main() {
    done1 := make(chan bool)
    done2 := make(chan bool)
 
    go run1(done1)
    go run2(done2)
 
EXIT:
    for {
        select {
        case <-done1:
            println("run1 완료")
 
        case <-done2:
            println("run2 완료")
            break EXIT
        }
    }
}
 
func run1(done chan bool) {
    time.Sleep(1 * time.Second)
    done <- true
}
 
func run2(done chan bool) {
    time.Sleep(2 * time.Second)
    done <- true
}
```