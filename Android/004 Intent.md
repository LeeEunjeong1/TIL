# Intent
## 웹페이지 이동
```Kotlin
startActivity(Intent(Intent.ACTION_VIEW,Uri.parse("주소입력")))
```
## Activity 이동
```Kotlin
val intent = Intent(this,NextActivity::class.java) // Activity 경우
val intent = Intent(requireContext(),NextActivity::class.java) // Fragment 경우
intent.putExtra("name",name) // 넘길 값
startActivity(intent)

//NextActivity에서 값 받을 때
val getName = intent.getStringExtra("name")
```
> 잊기 전에 메모