# Elvis Operation
```Kotlin
str?.length ?: -1
```
str?.length 객체가 null이 아니면 그 값을 리턴하고, null이면 -1을 리턴한다.
# Safe call
```Kotlin
str?.length
```
str 객체가 null일 때 null을 리턴하고, null이 아닐 때는 str.length를 리턴한다.<br><br>

>https://kotlinlang.org/docs/null-safety.html#elvis-operator