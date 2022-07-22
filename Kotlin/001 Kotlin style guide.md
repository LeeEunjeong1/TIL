# Kotlin Style Guide

## 소스파일
## 이름지정
- 소스파일에 최상위 클래스가 하나 뿐일 경우 : 이름에 대소문자를 구분하는 이름과 .kt 확장자가 반영되어야 한다.

```kotlin
// MyClass.kt
class MyClass { }

// Bar.kt
class Bar { }
fun Runnable.toBar(): Bar = // …
```
## 구조
.kt 파일 순서
- 저작권 및 / 또는 라이선스 헤더(선택사항)
- 파일 수준 주석
- Package 문
- Import 문
- 최상위 수준 선언
## 저작권 / 라이선스
파일에 저작권 또는 라이선스 헤더가 포함된 경우 맨위에 여러 줄로 주석을 넣어야 한다.
```
/*
 * Copyright 2017 Google, Inc.
 *
 * ...
 */
 ```

# 서식
## 중괄호
else 분기가 2개 이상이 아니고 한 줄에 들어가는 when 분기 및 if 문 본문에는 중괄호가 필요하지 않는다.
```kotlin
if (string.isEmpty()) return

val result =
    if (string.isEmpty()) DEFAULT_VALUE else string

when (value) {
    0 -> return
    // …
}
```
if, for, when 분기, do 및 while 문의 경우 본문이 비어 있거나 단일 구문만 포함하는 경우에도 중괄호가 필요하다.
```kotlin
if (string.isEmpty())
    return  // WRONG!

if (string.isEmpty()) {
    return  // Okay
}
```
비어 있지 않은 블록과 블록 형식 구문에서는 중괄호가 K&R 스타일을 따른다. 
```kotlin
return Runnable {
    while (condition()) { // 여는 중괄호 앞에 줄바꿈X
        foo() // 여는 중괄호 뒤에 줄바꿈O
    } // 닫는 중괄호 앞에 줄바꿈O
}

return object : MyClass() {
    override fun foo() {
        if (condition()) {
            try {
                something()
            } catch (e: ProblemException) {
                recover()
            }
        } else if (otherCondition()) {
            somethingElse()
        } else { // 중괄호 뒤에 else 오면 줄바꿈X
            lastThing()
        }
    }
}
```
```
try {
    doSomething()
} catch (e: Exception) {} // WRONG!

try {
    doSomething()
} catch (e: Exception) {
} // Okay
```
## 공백
언어 또는 다른 스타일 규칙에 필요할 때와 리터럴, 주석 및 KDoc를 제외하면 단일 ASCII 공백이 다음 위치에만 표시된다.

```kotlin
// WRONG!
for(i in 0..1) {
}
// Okay
for (i in 0..1) {
}
```
```kotlin
/* 예약어(else or catch) */
// WRONG!
}else {
}
// Okay
} else {
}
```
```kotlin
// WRONG!
if (list.isEmpty()){
}
// Okay
if (list.isEmpty()) {
}
```
```kotlin
// WRONG!
val two = 1+1
// Okay
val two = 1 + 1
```
```kotlin
// WRONG!
ints.map { value->value.toString() }
// Okay
ints.map { value -> value.toString() }
```
예외 - 멤버 참조의 두 콜론 (::) , 점 구분자(.) , 범위 연산자(..)
```kotlin
// WRONG!
val toString = Any :: toString
// Okay
val toString = Any::toString

// WRONG
it . toString()
// Okay
it.toString()

// WRONG
 for (i in 1 .. 4) print(i)
// Okay
 for (i in 1..4) print(i)
 
```

## 이름 지정
패키지 이름은 모두 소문자, 연속 단어는 밑줄 없이 연결된다
```kotlin
// Okay
package com.example.deepspace
// WRONG!
package com.example.deepSpace
// WRONG!
package com.example.deep_space
```
클래스 이름은 PascalCase (명사 또는 명사구), 공백 포함X
```kotlin
Character
ImmutableList
```
인터페이스 이름은 명사 또는 명사구이지만 형용사구를 대신 사용하는 경우도 있다
```kotlin
List // 명사구
Readable // 형용사구
```
함수 이름은 camelCase (동사 또는 동사구)
```kotlin
fuhn sendMessage()
fun stop()
```
이름의 논리적 구성요소를 구분하기 위해 테스트 함수 이름에 밑줄을 표시할 수 있다.
```kotlin
@Test fun pop_emptyStack() {
    // …
}
```
상수 이름에는 UPPER_SNAKE_CASE를 사용하여 밑줄로 단어를 구분한다. 
```kotlin
const val NUMBER = 5
val NAMES = listOf("Alice", "Bob")
val AGES = mapOf("Alice" to 35, "Bob" to 32)
val COMMA_JOINER = Joiner.on(',') // Joiner is immutable
val EMPTY_ARRAY = arrayOf()
```
상수가 아닌 이름은 camelCase로 작성된다. 
```kotlin
//인스턴스 속성, 로컬 속성, 매개변수 이름에 적용된다.

val variable = "var"
val nonConstScalar = "non-const"
val mutableCollection: MutableSet = HashSet()
val mutableElements = listOf(mutableInstance)
val mutableValues = mapOf("Alice" to mutableInstance, "Bob" to mutableInstance2)
val logger = Logger.getLogger(MyClass::class.java.name)
val nonEmptyArray = arrayOf("these", "can", "change")
```
지원 속성이 필요한 경우 밑줄처리된 접두사를 제외하고 이름이 실제 속성의 이름과 정확히 일치해야 한다.
```kotlin
private var _table: Map? = null

val table: Map
    get() {
        if (_table == null) {
            _table = HashMap()
        }
        return _table ?: throw AssertionError()
    }    
```    

> 한 번 정리할 필요가 있었다.. 내코드... <br>
참고 : https://developer.android.com/kotlin/style-guide