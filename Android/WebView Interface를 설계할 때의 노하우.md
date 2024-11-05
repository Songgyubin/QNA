최근 사이드 프로젝트를 하면서 WebView와 App 간의 Interface를 구축해서 통신해야하는 상황이 있었습니다. 

정말 간단하게 Toast를 띄우는 형식이라 다음과 같이 코드를 작성했는데요.

```kotlin
class WebViewAppInterface(
	private val onShowToast: (String) -> Unit
) {

	@JavascriptInterface
	fun showToast(message: String) {
		onShowToast(message)
	}
}
```

좀 더 큰 규모의 WebView Interface를 설계할 때의 노하우가 있으신지 궁금합니다!