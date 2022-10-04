# MDV Bank Aggregation Documentation

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
    
      1. Customizing Account Card
         
         # Id's include
         
         #al-account-card : ID for the parent div, can be used to customise the background color of the account card.
         
         #al-account-card--account-name : Used to customize the style for the account name.
         
         #al-account-card--account-balance: Change the style for account balance text.
         
         #al-account-card--account-number: Change the style for account number.
         
         #al-account-card--account-type: Change the style for account type.
         
         Example of how you can customize account card
         
         ```
         css
         
         #al-account-card{
            background:#FFFF00;
         }
         
         #al-account-card--account-balance{
            color: #000000;
            font-size: 16px;
            font: 1.2em "Fira Sans", sans-serif;
         }
         
         ```
      2. Customize Transaction Card
      
         # Id's include:
         
         #al-transaction-card : ID for the parent div, can be used to customise the background color of the transaction card.
         
         #al-transaction-card--merchant-name : Used to customize the style for the transaction merchant name.
         
         #al-transaction-card--category-name: Change the style for the transaction category name.
         
         #al-transaction-card--date: Change the style for transaction date.
         
         #al-transaction-card--amount: Change the style for transaction amount.
         
         Example of how you can customize transaction card
         
         ```
         css
         
         #al-transaction-card{
            background:#FFFF00;
         }
         
         #al-transaction-card--amount{
            color: #000000;
            font-size: 16px;
            font: 1.2em "Fira Sans", sans-serif;
         }
         
         ```
         
      3. Customize the balance view section

         # Id's include:

         #al-balance-view : ID for the parent div, can be used to customise the background color of the balance view section.

         #al-balance-title : Used to customize the style for balance view title.
         #al-balance-amount : Used to customize the style for balance view amount.

         Example of how you can customize balcance view section

         ```
         css

         #al-balance-view{
            background:#FFFF00;
         }

         #al-balance-amount{
            color: #000000;
            font-size: 16px;
            font: 1.2em "Fira Sans", sans-serif;
         }

         ```
            
         
         
         
         
         
      
