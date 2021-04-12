# **구초제 (Struct)**
**Go**에서 **struct**는 **Custom Data Type**을 표현하는데, 사용되는데, **Go**의 **struct**는 필드들의 집합체이며 필드들이 컨테이너이다.

**Go**에서 **struct**는 필드 데이타만을 가지며, 메서드를 갖지 않는다. 

## **Struct 선언**
**struct**를 정의하기 위해서는 **Custom Type**을 정의하는데 사용하는 **type**문을 사용한다.

### **코드**
``` go
package main
 
import "fmt"
 
// struct 정의
type person struct {
    name string
    age  int
}
 
func main() {
    // person 객체 생성
    p := person{}
     
    // 필드값 설정
    p.name = "Lee"
    p.age = 10
     
    fmt.Println(p)
}
```

## **Struct 객체 생성**
선언된 **struct** 타입으로부터 객체를 생성하는 방법은 몇 가지 방법들이 있다.

* 객체를 먼저 할당하고, 나중에 그 필드값을 채워넣는 방법

    ``` go
    var p1 person
    p1.name = "명철" // . 을 사용하여 접근한다.
    ```

* **Struct** 객체를 생성할 때, 초기값을 함께 할당하는 방법도 있다. 

    ``` go
    var p1 person 
    p1 = person{"Bob", 20}
    p2 := person{name: "Sean", age: 50} // 순서와 상관없이 필드명을 지정하여 할당할 수 있다.
    ```

만약 일부 필드가 생략될 경우 생략된 필드들은 **Zero value**를 갖는다.

### **new() 함수 사용**
**new()**를 사용하면 모든 필드는 **Zero value**로 초기화 하면 **객체의 포인터를 리턴**한다.

객체 포인터인 경우에도 필드 엑세스 시 **.** 을 사용하는데, 이때 포인터는 자동으로 **Dereference** 된다.

### **예제**
``` go
p := new(person)
p.name = "Lee"
```

**Go**에서 **struct**는 기본적으로 **mutable** 개체로서 필드값이 변화할 경우 해당 개체 메모리에서 직접 변경된다.
* **struct** 객체를 다른 함수의 파라미터로 넘긴가면, **Call By Value**에 따라 **객체를 복사**해서 전달하게 된다.
* 만약 **Call By Reference**로 **struct**를 전달 하고자 한다면, **포인터로 전달**해야 한다.

## **생성자 함수**
구조체의 필드가 사용 전에 초기화되어야 하는 경우가 있다. 

## **코드**
``` go
package main
 
type dict struct {
    data map[int]string
}
 
//생성자 함수 정의
func newDict() *dict {
    d := dict{}
    d.data = map[int]string{}
    return &d //포인터 전달
}
 
func main() {
    dic := newDict() // 생성자 호출
    dic.data[1] = "A"
}
```