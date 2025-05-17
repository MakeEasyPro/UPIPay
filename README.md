UPIPay is a manual UPI based payment gateway provided by MakeEasy.

**STEPS-**
1. Download **MakeEasy** app from playstore. Click top right corner and create an account. Login and collect the **merchant id**.
2. Open your project create libs folder and paste **UPIPay.aar** and implement as dependency file in build.gradle (app)

`implementation(files("libs/UPIPay.aar"))`

```kotlin

//Initialize the UPIPayFlow class
val upiPayFlow = UPIPayFlow(this)

// Create Order Id
val orderId = UPIPayUtils.createOrderId()

// Define UPIPayUser model class
val user = UPIPayUser("2")

// Setup UPIPayFlow UI design
val uiDark = UPIPayUI()
uiDark.appLogo = R.drawable.ebet
uiDark.appName = getString(R.string.app_name)
uiDark.theme = UPIPayUtils.THEME_LIGHT //UPIPayUtils.THEME_DARK
uiDark.merchantId = UPIPayUtils.DEMO_MERCHANT_ID
//uiDark.webhook = "your_webhook_url"
//uiDark.alertKey = "your_tg_group_username"

// Define UPIPayModel model class
val upiPayModel = UPIPayModel("Payee Name","100",orderId,"your_upi_id",user)

// Pass the mandatory objects and ready for payment
upiPayFlow.init(upiPayModel,uiLight,object:UPIPayInitListener {
    override fun onSuccess() {
        upiPayFlow.startFlow()
    }
    override fun onFailed(p0: Int, p1: String?) {
        Toast.makeText(this@MainActivity,p1,Toast.LENGTH_SHORT).show()
    }

})
```
