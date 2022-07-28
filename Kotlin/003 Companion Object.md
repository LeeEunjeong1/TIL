# Companion Object
## JAVA Static
- 클래스 멤버임을 지정하기 위해 사용
- static이 붙은 변수와 메소드를 각각 클래스 변수, 클래스 메소드라고 부른다.
- static이 붙지 않은 클래스 내의 변수와 메소드는 각각 인스턴스 변수, 인스턴스 메소드라고 부른다.
- static이 붙은 멤버는 클래스가 메모리에 적재될 때 자동으로 함께 생성되므로 인스턴스 생성 없이 클래스 명 다음에 점(.)을 쓰면 바로 참조할 수 있다.

## Kotlin Companion Object
### Companion object는 static이 아니다.
- companion object{}는 클래스가 메모리에 적재되면서 함께 동반(companion)되는 객체
- 이 동반 객체는 클래스명.Companion으로 접근할 수 있다.
- 클래스명. 으로 축약이 가능하다. (이 때문에 static으로 착각)
### Comapanion object는 객체이다.
- 변수에 할당 가능 (static 은 불가능)
``` Kotlin
    calss MyClass{
        companion object{
            val prop = "hello"
        }
    }
    fun main(){
        val comp = MyClass.Companion
        println(comp.prop)
    }    
```
### Comapnion object는 Class당 하나
### Comapnion object에 이름을 지을 수도 있다.
```Kotlin
companion object MyCompanion{

}
```
### Companion object는 인터페이스 내에서도 정의할 수 있다.

#
> 참고 : https://www.bsidesoft.com/8187