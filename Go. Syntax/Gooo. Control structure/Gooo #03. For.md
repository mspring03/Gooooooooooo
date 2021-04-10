# **For**

## **for 문**
Go 프로그래밍 언어에서 반복문은 for 루프를 이용한다.
* Go는 반복문이 for 밖에 없다 ㅋㅋ

### **형식**
```
for 초기값; 조건식; 증감 { ... }
```
* 괄호는 생략한다. 

<br>

### **예제**
``` go
sum := 0
for i := 1; i <= 100; i++ {
    sum += i
}
println(sum)
```

<br>

## **조건식만 쓰는 for 루프**
Go언어에서 for 루프는 초기값과 증갑식을 생략하고 조건식만 사용할 수 있다. 
* 이는 for 루프가 while 루프와 같이 쓰이도록 한다.  

### **예제**
``` go
n := 1
for n < 100 {
    n *= 2      
    //if n > 90 {
    //   break 
    //}     
}
println(n)
```

## **무한루프**
for 루프로 무한루프로 만들려면 초기값, 조건식, 증감을 모두 생략하면 된다.

### **예제**
``` go
for {
    println("Infinite loop")        
}
```

## **for range 문** 
for range 문은 컬렉션으로 부터 한 요소씩 가져와 차례로 for 블럭의 문장을 실행한다.  

### **형식**
```
for 인덱스, 요소값 := range 컬렉션
```

### **예제**
``` go
names := []string{"홍길동", "이순신", "강감찬"}
 
for index, name := range names {
    println(index, name)
}
```

### **출력**
```
0 홍길동
1 이순신
2 강감찬
```

## **제어**
경우에 따라 for 루프를 제어할수 있다.
* break: for 루프를 탈출한다
* continue: for 루프 시작부분으로 이동한다.
* goto: for 루프와 상관없이 이동한다.

### **예제**
``` go
func main() {
    var a = 1
    for a < 15 {
        if a == 5 {
            a += a
            continue // for루프 시작으로
        }
        a++
        if a > 10 {
            break  //루프 빠져나옴
        }
    }
    if a == 11 {
        goto END //goto 사용예
    }
    println(a)
 
END:
    println("End")
```

## **레이블**
레이블을 지정하여 break, continue, goto를 사용하여 지정된 레이블로 이동할 수도 있다.

### **예제**
``` go
package main
 
func main() {
    i := 0
 
L1:
    for {
     
        if i == 0 {
            break L1
        }
    }
 
    println("OK")
}
```