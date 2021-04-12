# **메서드 (Method)**
Go 메서드는 특별한 형태의 func 함수이다.

### **메서드 선언 방법**
``` go
func ("필드값을 가져올 변수" "구조체 타입(이름)") 함수명() 리턴타입 {}
```

### **코드**
``` go
package main
 
//Rect - struct 정의
type Rect struct {
    width, height int
}
 
//Rect의 area() 메소드
func (r Rect) area() int {
    return r.width * r.height   
}
 
func main() {
    rect := Rect{10, 20}
    area := rect.area() //메서드 호출
    println(area)
}
```

## **Value receiver / Pointer receiver**
**Value receiver**는 **struct**의 데이터를 복사하여 전달하며, **포인터 receiver**는 **struct**의 포인터만을 전달한다.

**value receiver**의 경우 만약 메서드 내에서 그 **struct**의 필드값이 변경되더라도 호출자의 데이타는 변경되지 않는 반면, **포인터 receiver**는 메서드 내의 필드값 변경이 그대로 호출자에서 반영된다.

### **코드** 
``` go
// 포인터 Receiver
func (r *Rect) area2() int {
    r.width++
    return r.width * r.height
}
 
func main() {
    rect := Rect{10, 20}
    area := rect.area2() //메서드 호출
    println(rect.width, area) // 11 220 출력
}
```