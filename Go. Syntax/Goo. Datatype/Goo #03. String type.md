# **문자열 (String)**
문자열은 **Golang**의 읽기 전용 바이트 조각이다.
문자열은 두가지 방법으로 초기화 가능하다.

* **큰 따옴표** 사용 "" 예: "this"

**큰 따옴표** 안의 문자열은 **escape sequences**를 따릅니다.
예를 들어, 문자열에서 /n을 포함하고 있으면 새 라인에서 출력을 하게 된다. 

하지만 **뒷 따옴표**의 경우 문자열은 원시 문자열일 뿐 탈출 순서를 존중하지 않는다.

* **뒷 따옴표** 사용 `` 예: `eg\nthis`

---

문자열의 각 문자는 일부 바이트를 차지한다.  
예를 들어 **utf-8** 인코딩 문자열의 경우 각 문자는 1~4바이트를 차지한다.

**utf-8**에서, 문자 파운드 기호 £가 2바이트를 사용하여 인코딩되는 동안, 문자 a또는 b는 1바이트로 인코딩 된다.  
따라서 문자열은 바이트 배열로 변환하여 아래와 같이 인쇄할때 "ab£" 문자열은 4바이트를 출력한다.
``` go
s := "ab£"
fmt.Println([]byte(s))
```

### **출력**
``` go
[48 98 194 163]
```

또한 len("ab£")을 사용하여 문자열 길이를 인쇄하려고 할 때 4바이트가 포함되어 있으므로 3이 아니라 4가 출력된다.

또한 각 문자를 형성하는 **sequences of byte**에 걸쳐 범위가 루프된다.
``` go
s := "ab£"
for _, c =: range s {
    fmt.Println(string(c))
}
```

### **출력**
``` go
a b £
```

문자열에서 수행할 수 있는 작업이 많다.  
이러한 작업중 하나는 두 문자열의 연결이다.  
기호 '**+**'는 두 문자를 연결해준다.

``` go
x := "this\nthat"
fmt.Printf("x is: %s\n", x)

y := `this\nthat`
fmt.Printf("y is: %s\n", y)
s := "ab£"

fmt.Println([]byte(s))

fmt.Println(len(s))

for _, c := range s {
    fmt.Println(string(c))
}

fmt.Println("c" + "d")
```

### **출력**
``` go
x is: this
that
y is: this\nthat
[97 98 194 163]
4
a
b
£
cd
```