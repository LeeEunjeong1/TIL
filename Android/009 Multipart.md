눈물의 Multipart 기록

### 소소한 헤맨 과정
1. @PartMap data: HashMap<String, RequestBody> PartMap으로 String, RequestBody값 넣기 -> 실패
https://velog.io/@1106laura/Retrofit%EC%97%90%EC%84%9C-Multipart-%EC%84%9C%EB%B2%84-%ED%86%B5%EC%8B%A0-with-Kotlin <br>
참고했는데.. 완전 똑같은데..왜 안돼...<br>
2.  @Part content: RequestBody 값 하나하나 RequestBody값으로 넣기 -> 실패<br>


### 해결 방법
서버내에 있는 형식이 달랐나보다. 
https://jungwoon.github.io/android/retrofit/2021/02/02/Retrofit-File-Upload.html <br>
해당 블로그에서 착안을 해서!! <br>

```kotlin
@Part content: MultipartBody.Part
val content : MultipartBody.Part = MultipartBody.Part.createFormData("content",content_et.value.toString())
```
file만 MultipartBody.Part로 보냈었는데, 다른 값들도 MultipartBody.Part로 보냄

역시 해결하고 보면 간단한 코딩.. 이래서 좋다..(진짜)