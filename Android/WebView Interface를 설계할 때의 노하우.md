# Android WebView 사용 사례

### 기본적인 사용 사례

```kotlin
// WebViewAppInterface 정의
class WebViewAppInterface(private val context: Context) {

    @JavascriptInterface
    fun showToast(message: String) {
        // 예시: 토스트 메시지 표시
        Toast.makeText(context, message, Toast.LENGTH_SHORT).show()
    }
}

// WebViewResourceManager 정의
class WebViewResourceManager(private val webView: WebView) {

    fun initializeWebViewSettings() {
        val webSettings = webView.settings

        // WebView 설정 초기화
        webSettings.javaScriptEnabled = true // JavaScript 활성화
        webSettings.cacheMode = WebSettings.LOAD_CACHE_ELSE_NETWORK // 캐시 모드 설정
        webSettings.defaultTextEncodingName = "utf-8" // 텍스트 인코딩 설정

        // WebViewClient 및 WebChromeClient 설정 (필요시 추가)
        webView.webViewClient = android.webkit.WebViewClient()
        webView.webChromeClient = android.webkit.WebChromeClient()
    }

    fun setupJavascriptInterface(context: Context) {
        // addJavascriptInterface 설정
        webView.addJavascriptInterface(WebViewAppInterface(context), "AndroidInterface")
    }
}

// MainActivity에서 사용 예제
class MainActivity : AppCompatActivity() {

    private lateinit var webView: WebView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // WebView 초기화
        webView = findViewById(R.id.webView)

        // WebViewResourceManager로 관리
        val resourceManager = WebViewResourceManager(webView)
        resourceManager.initializeWebViewSettings()
        resourceManager.setupJavascriptInterface(this)

        // 로드할 URL 지정
        webView.loadUrl("file:///android_asset/sample.html")
    }
}
```

### WebView를 적용할 때 클린아키텍처를 적용하는 것은 어떤가?

적용한다면 하위 Layer에서 핵심 url 및 정보들을 관리할 순 있겠으나, UI와 관련된 내용들이기 때문에
Presentation Layer에서 Manager로 관리하는 것만으로도 충분할 것 같다는 의견이 나왔습니다.