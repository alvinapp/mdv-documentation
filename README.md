# MDV DOCUMENTATION
## A guide on how to integrate the mdv package into your mobile application
## Steps:

1. First create an account with us on Alvin Enterprise Dashboard to obtain a public key and email that will be used to authenticate you for MDV embeddable    widget.
2. Congrats!! Now that you have your account ready, its time to load the MDV embeddable widget into your mobile app. In our case we shall embed the widget      into your app through a webview.

   ## Embed the webview
   
   ### Android app
   
   1. To load the webview url in your app, you should append the public key and email obtained after you register an account on the enterprise dashboard,
      as parameters like this -> http://example-url/?publicKey=xxxxxx&email=example@gmail.com

   2. Initialize the webview inside your app

      ### Kotlin
      
   ```
   class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val myWebView = findViewById<View>(R.id.mdv_web_view) as WebView
        myWebView.webChromeClient = object : WebChromeClient() {
            override fun onConsoleMessage(message: ConsoleMessage): Boolean {
                Log.d(
                    "SampleApp", "${message.message()} -- From line " +
                            "${message.lineNumber()} of ${message.sourceId()}"
                )
                return true
            }
        }
        val webSettings = myWebView.settings
        webSettings.javaScriptEnabled = true
        webSettings.loadWithOverviewMode = true
        webSettings.useWideViewPort = true
        webSettings.cacheMode = WebSettings.LOAD_DEFAULT
        val url = Uri.parse("http://52.72.25.150").buildUpon()
            .appendQueryParameter("publicKey", "xxxxxxxx")
            .appendQueryParameter("email", "example@gmail.com").build().toString()
        myWebView.loadUrl(url)
    }
   }
   ```
   
   ## Customizing styles for mdv components
   
   Inorder to customize the mdv component styles, we provide a way to customize whereby pass in a css link as a style parameter. This link is should point    to your custom css file. eg something like this:  https://static.staticsave.com/alvin/test.css
   
   # Procedure to customize
   1. Pass in your css link as a parameter see below:
   
      ```
       val url = Uri.parse("http://52.72.25.150").buildUpon()
         .appendQueryParameter("styleUrl","https://static.staticsave.com/alvin/test.css")
         .build().toString()
          myWebView.loadUrl(url)
          
       ```
    Inside your custom css, you should reference html ids to target various component section and override the styles for example
      1. Customizing account card
      
