# **Map**

## **Map 개요**
**Map**은 키에 대응하는 값을 신속히 찾는 **해시 테이블**을 구현한 **자료구조**이다.

**Go** 언어는 **Map** 타입을 내자하고 있는데,  "**map[Key타입]Value타입**" 과 같이 선언 가능하다.

<br>

## **선언**
``` go
var idMap map[int]string
```

이때 선언된 변수 idMap은 **nil**값을 갖으며, 이를 **Nil Map**이라고 부른다. 

**Nil map**에는 어떤 데이타를 쓸 수 없는데, **map**을 초기화하기 위해 **make()**함수를 사용할 수 있다.
``` go
idMap = make(map[int]string)
```
**make()** 함수의 첫번째 파라미터로 **map** 키워드와 **[키타입]값타입**을 지정하는데, 이때 **make()**함수는 해시테이블 자료구조를 메모리에 생성하고 그 메모리를 가리키는 **map value**를 리턴한다.

**map**은 **make()** 함수를 사용하여 초기화할 수도 있지만, 리터럴을 사용해 초기화 할 수도 있다.  

### **코드**
``` go
//리터럴을 사용한 초기화
tickers := map[string]string{
    "GOOG": "Google Inc",
    "MSFT": "Microsoft",
    "FB":   "FaceBook",
}
```

<br>

## **Map 사용**
처음 **map**이 **make()** 함수에 의해 초기화 되었을 때는, 아무 데이터가 없는 상태이다.  

이때 새로운 데이터를 추가하기 위해서는 "**map변수[키] = 값**" 과 같이 해당 키에 그 값을 할당하면 된다.

### **코드**
``` go
var m map[int]string

m = make(map[int]string)
//추가 혹은 갱신
m[901] = "Apple"
m[134] = "Grape"
m[777] = "Tomato"

// 키에 대한 값 읽기
str := m[134]
println(str)

noData := m[999] // 값이 없으면 nil 혹은 zero 리턴
println(noData)

// 삭제
delete(m, 777)
```

<br>

## **Map 키 체크**
**map**을 사용하는 경우 종종 **map**안에 특정 키가 존재하는지를 체크할 필요가 있다. 

이를 위해 **Go**에선 읽기를 수행 할때 2개의 리턴값을 리턴한다.
* 첫번째 리턴값: 키에 상응하는 값
* 두번째 리턴값: 키의 존재 여부를 나타내는 bool 값

### **코드**
``` go
tickers := map[string]string{
    "GOOG": "Google Inc",
    "MSFT": "Microsoft",
    "FB":   "FaceBook",
    "AMZN": "Amazon",
}

// map 키 체크
val, exists := tickers["MSFT"]
if !exists {
    println("No MSFT ticker")
}
```

<br>

## for 루프를 사용한 Map 열거
**Map**이 갖고 있는 모든 요소들을 출력하기 위해, **for range** 루프를 사용할 수 있다.

**Map** 컬렉션에 **for range**를 사용하면, **Map** 키와 **Map** 값 2개의 데이타를 리턴한다.

### **코드**
``` go
myMap := map[string]string{
    "A": "Apple",
    "B": "Banana",
    "C": "Charlie",
}

// for range 문을 사용하여 모든 맵 요소 출력
// Map은 unordered 이므로 순서는 무작위
for key, val := range myMap {
    fmt.Println(key, val)
}
```