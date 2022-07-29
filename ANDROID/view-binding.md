# ViewBinding 사용하기

## build.gradle(app) 설정하기
```
android {
    ...
    buildFeatures {
        viewBinding = true
    }
}
```

<br/>

## BaseFragment 만들기
```
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.fragment.app.Fragment
import androidx.viewbinding.ViewBinding

typealias Inflate<T> = (LayoutInflater, ViewGroup?, Boolean) -> T

abstract class BaseFragment<VB : ViewBinding>(private val inflate: Inflate<VB>) : Fragment() {

    private var _binding: VB? = null
    val binding get() = _binding!!

    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        _binding = inflate.invoke(inflater, container, false)
        return binding.root
    }

    override fun onDestroyView() {
        super.onDestroyView()
        _binding = null
    }
}
```

<br/>

## 사용법
```
class SampleFragment : BaseFragment<FragmentSampleBinding>(FragmentSampleBinding::inflate) {

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
    }
}
```

<br/>

# 참고
[안드로이드 개발 (29) Fragment에서 ViewBinding 사용 시 주의할 점](https://gift123.tistory.com/58)