# **Booleans**
데이터 유형은 **bool**이며 **true** 또는 **false** 두개의 값을 가지고 있다.

> default value: `false`

### **작업**
* And -> &&
* OR  -> ||
* 부정 -> !

### **예제**
``` go
var a bool
fmt.Printf("a's value is %t\n", a)

andOperation := 1 < 2 && 1 > 3
fmt.Printf("Ouput of AND operation on one true and other false %t\n", andOperation)

orOperation := 1 < 2 || 1 > 3
fmt.Printf("Ouput of OR operation on one true and other false: %t\n", orOperation)

negationOperation := !(1 > 2)
fmt.Printf("Ouput of NEGATION operation on false value: %t\n", negationOperation)
```

### **출력**
```
a's value is false
Ouput of AND operation on one true and other false false
Ouput of OR operation on one true and other false: true
Ouput of NEGATION operation on false value: true
```