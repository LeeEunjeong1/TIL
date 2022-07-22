# ViewBinding Library
뷰 결합 기능을 사용하면 뷰와 상호작용하는 코드를 쉽게 작성할 수 있다. 모듈에서 사용 설정된 뷰 결합은 모듈에 있는 각 XML 레이아웃 파일의 결합 클래스를 생성한다. 바인딩 클래스의 인스턴스에는 상응하는 레이아웃에 ID가 있는 모든 뷰의 직접 참조가 포함된다.

대부분의 경우 뷰 결합이 findViewById를 대체한다.
findViewId 이제 안녕~~~



## 설정
Build.gradle
```Kotlin
android {
        ...
        viewBinding {
            enabled = true
        }
    }
 ```
결합 클래스를 생성하는 동안 레이아웃 파일을 무시하려면 viewBindingIgnore 루트 뷰에 추가
```Kotlin
<LinearLayout
            ...
            tools:viewBindingIgnore="true" >
        ...
    </LinearLayout>
```
## 사용

모듈에 뷰 결합을 사용하도록 설정되면 모듈에 포함된 각 XML 레이아웃 파일의 결합 클래스가 생성된다. 각 결합 클래스에는 루트 뷰 및 ID가 있는 모든 뷰의 참조가 포함된다. 결합 클래스의 이름은 XML 파일의 이름을 카멜 표기법으로 변환하고 끝에 'Binding'을 추가하여 생성된다.

```Kotlin 
<LinearLayout ... >
        <TextView android:id="@+id/name" />
        <ImageView android:cropToPadding="true" />
        <Button android:id="@+id/button"
            android:background="@drawable/rounded_button" />
    </LinearLayout>
```    
### Activity에서 ViewBinding 사용하기!
1. 생성된 결합 클래스에 포함된 정적 inflate() 메서드를 호출합니다. 그러면 활동에서 사용할 결합 클래스 인스턴스가 생성된다.
2. getRoot() 메서드를 호출하거나 Kotlin 속성 구문을 사용하여 루트 뷰 참조를 가져온다.
3. 루트 뷰를 setContentView()에 전달하여 화면상의 활성 뷰로 만든다.
```Kotlin
    private lateinit var binding: ResultProfileBinding

    override fun onCreate(savedInstanceState: Bundle) {
        super.onCreate(savedInstanceState)
        binding = ResultProfileBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
        
        binding.name.text = vewModel.name
        binding.buttonetOnClickListener { viewModel.userClicked() }
    
    } 
```
### Fragment에서 ViewBinding 사용하기!
1. 생성된 결합 클래스에 포함된 정적 inflate() 메서드를 호출한다. 그러면 프래그먼트에서 사용할 결합 클래스 인스턴스가 생성된다.
2. getRoot() 메서드를 호출하거나 Kotlin 속성 구문을 사용하여 루트 뷰 참조를 가져온다.
3. onCreateView() 메서드에서 루트 뷰를 반환하여 화면상의 활성 뷰로 만든다.
```Kotlin
    private var _binding: ResultProfileBinding? = null
    // This property is only valid between onCreateView and
    // onDestroyView.
    private val binding get() = _binding!!

    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        _binding = ResultProfileBinding.inflate(inflater, container, false)
        val view = binding.root
        return view

        binding.name.text = viewModel.name
    binding.button.setOnClickListener { viewModel.userClicked() }
    
    }

    override fun onDestroyView() {
        super.onDestroyView()
        _binding = null
    }
```
## findViewById와 차이
뷰 결합에는 findViewById를 사용하는 것에 비해 다음과 같은 중요한 장점이 있습니다.

- Null 안전: 뷰 결합은 뷰의 직접 참조를 생성하므로 유효하지 않은 뷰 ID로 인해 null 포인터 예외가 발생할 위험이 없습니다. 또한 레이아웃의 일부 구성에만 뷰가 있는 경우 결합 클래스에서 참조를 포함하는 필드가 @Nullable로 표시됩니다.
- 유형 안전: 각 바인딩 클래스에 있는 필드의 유형이 XML 파일에서 참조하는 뷰와 일치합니다. 즉, 클래스 변환 예외가 발생할 위험이 없습니다.
이러한 차이점은 레이아웃과 코드 사이의 비호환성으로 인해 런타임이 아닌 컴파일 시간에 빌드가 실패하게 된다는 것을 의미합니다.

## DataBinding과 차이
ViewBinding과 DataBinding은 모두 뷰를 직접 참조하는 데 사용할 수 있는 결합 클래스를 생성합니다. 하지만 ViewBinding은 보다 단순한 사용 사례를 처리하기 위한 것이며 DataBinding에 비해 다음과 같은 이점을 제공합니다.

- 더 빠른 컴파일: ViewBinding에는 주석 처리가 필요하지 않으므로 컴파일 시간이 더 짧습니다.
- 사용 편의성: ViewBinding에는 특별히 태그된 XML 레이아웃 파일이 필요하지 않으므로 앱에서 더 신속하게 채택할 수 있습니다. 모듈에서 ViewBinding을 사용 설정하면 모듈의 모든 레이아웃에 ViewBinding이 자동으로 적용됩니다.

반대로 ViewBinding에는 DataBinding과 비교할 때 다음과 같은 제한사항이 있습니다.

ViewBinding은 레이아웃 변수 또는 레이아웃 표현식을 지원하지 않으므로 XML 레이아웃 파일에서 직접 동적 UI 콘텐츠를 선언하는 데 사용할 수 없습니다.

ViewBinding은 양방향 DataBinding을 지원하지 않습니다.
위 사항을 고려할 때 일부 사례에서 프로젝트에 ViewBinding과 DataBinding을 모두 사용하는 것이 가장 좋습니다. 고급 기능이 필요한 레이아웃에는 DataBinding을, 고급 기능이 필요 없는 레이아웃에는 ViewBinding을 사용할 수 있습니다.


# DataBinding Library
선언적 형식으로 레이아웃의 UI 구성요소를 앱의 데이터 소스와 결합할 수 있는 지원 라이브러리이다.<br>

### findViewById()
findViewById()를 호출하여 TextView 위젯을 찾아 viewModel 변수의 userName 속성에 결합

```Kotlin 
    findViewById<TextView>(R.id.sample_text).apply {
        text = viewModel.userName
    }

```
### Data Binding
레이아웃 파일에서 직접 위젯에 텍스트를 할당하는 방법
```Kotlin
<TextView
        android:text="@{viewmodel.userName}" />
```


레이아웃 파일에서 구성요소를 결합하면 활동에서 많은 UI 프레임워크 호출을 삭제할 수 있어 파일이 더욱 단순화되고 유지관리 또한 쉬워진다. 앱 성능이 향상되며 메모리 누수 및 null 포인터 예외를 방지할 수 있다.

- 참고: 대부분의 경우 뷰 결합은 구현은 더 간단하고 성능은 더 우수하면서도 데이터 결합과 동일한 이점을 제공합니다. findViewById() 호출을 대체할 때 주로 데이터 결합을 사용하는 경우 뷰 결합을 대신 사용해 보십시오.

> viewBinding하고 DataBinding 차이가 뭔지 몰랐는데, 나는 그냥 viewBinding만 쓰는 사람이었더랬다. ^^;
