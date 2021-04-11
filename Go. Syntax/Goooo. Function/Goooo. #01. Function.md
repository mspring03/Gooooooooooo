# **함수 (Function)**
## **함수**
>함수는 여러 문장을 묶어서 실행하는 코드 블럭의 단위이다.

<br>

### **함수 선언 방법**
```
func 함수명(파라미터) (리턴타입) {}
``` 

### **코드**
``` go
func main() {
    msg := "Hello"
    say(msg)
}
 
func say(msg string) {
    println(msg)
}
```

<br>

## **Call By Value**
위에 코드에서 msg의 값을 문자열이 복사되어 함수 say()에 절달된다.  

파라미터 msg의 값이 say() 함수 내에서 변경된다 하더라도 호출함수 main()에서는 변경되지 않는다.

<br>

## **Call By Reference**
변수 앞에 **&** 부호를 붙이면 msg변수의 주소를 표시하게 된다. 

흔하게 포인터라고 불리는 **&** 를 사용하면 함수에 msg 변수의 값을 복사하지 않고 msg 변수의 주소를 전달하게 된다. 

피호출 함수에서는 ***string** 과 같이 파라미터가 포인터임을 표시한다. 

여기서 파라미터 앞에 *를 붙이는데 이를 **Dereferenciing** 이라 한다. 

### **코드**
``` go
func main() {
    msg := "Hello"
    say(&msg)
    println(msg) //변경된 메시지 출력
}
 
func say(msg *string) {
    println(*msg)
    *msg = "Changed" //메시지 변경
}
```

<br>

## **Variadic Function (가변인자함수)**
함수에 고정된 수의 파라미터들을 전달하지 않고 다양한 숫자의 파라미터를 전달하고자 할 때 가변 파라미터를 나타내는 **...** 를 사용한다.

### **코드**
``` go 
func main() {   
    say("This", "is", "a", "book")
    say("Hi")
}
 
func say(msg ...string) {
    for _, s := range msg {
        println(s)
    }
}
```

<br>

## **함수 리턴값**
**Go** 언어는 복수개의 값을 리턴할 수 있다. 
### **코드**
``` go
func main() {
    count, total := sum(1, 7, 3, 5, 9)
    println(count, total)   
}
 
func sum(nums ...int) (int, int) {
    s := 0      // 합계
    count := 0  // 요소 갯수
    for _, n := range nums {
        s += n
        count++
    }
    return count, s
}
``` 

**Go**는 **Named Return Parameter** 라는 기능을 제공하여 리턴되는 값들을 **리턴파라미터**에 할당할 수 있는 기능이다. 

### **코드**
``` go
func main() {
	fmt.Println(sum(1, 2, 3, 4, 5)) // 5 15
}

func sum(nums ...int) (count int, total int) {
	for _, n := range nums {
		total += n
	}
	count = len(nums)
	return
}
```

리턴되는 값이 있을 경우에는 **return**문을 생략할수 없다.