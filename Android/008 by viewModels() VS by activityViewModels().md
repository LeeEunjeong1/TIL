### by viewModels()
- private val postViewModel : PostViewModel by viewModels()
- Fragment에 종속된다.

### by activityViewmodels()
- private val PostViewModel : postViewModel by activityViewModels()
- Fragment들의 부모가 되는 Activity의 뷰모델을 공유하게 된다. 
- 한 액티비티에서 파생된 프래그먼트들 끼리는 뷰모델을 공유할 수 있다. 데이터 공유 가능