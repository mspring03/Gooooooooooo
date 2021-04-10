# **If**
**if** 문은 해당 조건이 맞으면 **{}** 블럭안에 내용을 실행한다.  

**Go**의 **if** 조건문은 아래 예제에서 보듯이 조건식을 **괄호()**로 둘러 싸지 않아도 된다.

마지막으로 주목할 점은 **if** 문의 조건식은 반드시 **Boolean** 식으로 표현되어야 한다는 것이다. 
``` go
if k == 1 {  //시작 브레이스와 if문과 같은라인
    println("One")
}

```

**if** 문은 **else of**, 혹은 **else** 문을 함께 가질 수 있다.

``` go
if k == 1 {
    println("One")
} else if k == 2 { // 같은 라인
    println("Two")
} else { // 같은 라인
    println("Other")
}
```

**if** 문에서 조건식을 사용하기 이전에 간단한 문장을 함께 실행할 수 있다.
``` go 
if val := i * 2; val < max {
    println(val)
}
 
// 아래 처럼 사용하면 Scope 벗어나 에러
val++
```