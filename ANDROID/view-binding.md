# ViewBinding 사용하기

## build.gradle(app) 설정하기
확장자가 없는 id_rsa 파일은 개인키이고, id_rsa.pub처럼 .pub 확장자가 있는 파일은 공개키이다.
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

# 참고
[안드로이드 개발 (29) Fragment에서 ViewBinding 사용 시 주의할 점](https://gift123.tistory.com/58)