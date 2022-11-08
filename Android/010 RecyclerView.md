
### RecycerView 데이터 중복 현상 해결

-- recyclerView 스크롤시 이미지가 복제되는 현상 발생
-- recyclerView 스크롤시 데이터 중복 현상 발생

어댑터에 adapter.setHasStableIds(true)가 true이고 getItemId가 재정의되지 않았기 때문이라고 생각합니다. 따라서 recyclerView는 동일한 ID를 가진 홀더를 찾아 재사용하려고 합니다.

```kotlin
  // onBindViewHolder position 값 고정
    override fun getItemViewType(position: Int): Int {
        return position
    }
    override fun getItemId(position: Int): Long {
        return position.toLong()
    }
```

position 값을 고정하여 position에 고유 데이터 연결해주자.

https://stackoverflow.com/questions/32706246/recyclerview-adapter-and-glide-same-image-every-4-5-rows
