UPIPay is a manual UPI based payment gateway provided by MakeEasy.

**STEPS-**
1. Download **MakeEasy** app from playstore. Click top right corner and create an account. Login and collect the **merchant id**.
2. Open your project create libs folder and paste **UPIPay.aar** and implement as dependency file in build.gradle (app)

`implementation(files("libs/UPIPay.aar"))`

```kotlin
val upiPayFlow = UPIPayFlow(this)

        val orderId = UPIPayUtils.createOrderId()
        val user = UPIPayUser("2")

        val uiDark = UPIPayUI()
        uiDark.appLogo = R.drawable.ebet
        uiDark.appName = getString(R.string.app_name)
        uiDark.theme = UPIPayUtils.THEME_LIGHT
        uiDark.merchantId = UPIPayUtils.DEMO_MERCHANT_ID
        //uiDark.webhook = "your_webhook_url"
        //uiDark.alertKey = "your_tg_group_username"

        val uiLight = UPIPayUI()
        uiLight.appLogo = R.drawable.ebet
        uiLight.appName = getString(R.string.app_name)
        uiLight.theme = UPIPayUtils.THEME_DARK
        uiLight.merchantId = UPIPayUtils.DEMO_MERCHANT_ID
        //uiLight.webhook = "your_webhook_url"
        //uiLight.alertKey = "your_tg_group_username"

        findViewById<Button>(R.id.pay_button1).setOnClickListener {
            val upiPayModel = UPIPayModel(
                "Payee Name",
                "100",
                orderId,
                "your_upi_id",
                user
            )
            upiPayFlow.init(upiPayModel,uiDark,object:UPIPayInitListener {
                override fun onSuccess() {
                    upiPayFlow.startFlow()
                }
                override fun onFailed(p0: Int, p1: String?) {
                    Toast.makeText(this@MainActivity,p1,Toast.LENGTH_SHORT).show()
                }

            })
        }
        findViewById<Button>(R.id.pay_button2).setOnClickListener {
            val upiPayModel = UPIPayModel(
                "Payee Name",
                "100",
                orderId,
                "your_upi_id",
                user
            )
            upiPayFlow.init(upiPayModel,uiLight,object:UPIPayInitListener {
                override fun onSuccess() {
                    upiPayFlow.startFlow()
                }
                override fun onFailed(p0: Int, p1: String?) {
                    Toast.makeText(this@MainActivity,p1,Toast.LENGTH_SHORT).show()
                }

            })
        }
```


