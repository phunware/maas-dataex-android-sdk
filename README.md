Data SDK [![Language](https://img.shields.io/badge/Kotlin-1.3-%234c20f0.svg)]() [![Release](https://img.shields.io/badge/Release-0.1.0-%234c20f0.svg)]()
=====
The `Data SDK` enables publishers/app developers to earn PhunCoin by incorporating the SDK into their applications and exposing their users to the PhunWallet application.

In addition to contributing users to the data SDK - developers can also send app usage events for users - and earn PhunCoin when app activity is used by brands as audiences.

An easy to use dashboard in the Phunware MaaS portal (maas.phunware.com) provides a dashboard for developers to see their balances and track engagement from their users into the ecosystem.

> ***<sub>note</sub>*** <br/>
>  `Data SDK` currently only supports Android for  **SDK 23**+.

<a id="installation"></a>
## Using Data SDK

### **Gradle**

If using Gradle, add the following to your build.gradle:

```gradle
maven {
    url "https://nexus.phunware.com/content/groups/public"
}
```

and the following to your app/build.gradle

```gradle
implementation "com.phunware.crypto:dataex:0.1.0"
```

***
<a id="usage-overview"></a>
## Usage Overview

### **Initialization**
The Data SDK will automatically be initialized when your application process starts.  You only need to initialize our MaaS Core SDK to proceed with using the Data SDK.

The Data SDK relies on Phunware Core SDK to provide application authentication with the Phunware MaaS suite and provides other built in useful features such as Analytics. In the MaaS portal, retrieve your application identifier, access key, signature key to initialize the Core SDK in your Application class's onCreate with the following:

```kotlin
// Your Application onCreate

PwCoreSession.getInstance().registerKeys(this,
            "<my_appid>",
                "<my_accesskey>",
                "<my_signaturekey>"
```

***
### **Tease your users**

In order for your users to claim any accrued digital assets and receive the full benefit of participating in the PhunCoin ecosystem, they will have to install the PhunWallet mobile app.  We provide you a colorful platform specific widget that you can display anywhere in your app to call attention to installing the PhunWallet mobile app.

Publishers who successfully get their users to generate a Wallet in the PhunWallet mobile app will earn PhunCoin for each unique user.


```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.phunware.dataex.ui.TeaserView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

</LinearLayout>
```

***
Data SDK branding doesn't match your app? We gotchu.


```xml
<com.phunware.dataex.ui.TeaserView
            android:id="@+id/teaserSunshine"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:dataexBackground="@color/sunBackground"
            app:dataexForegroundTint="@color/sunForeground" />
```

***
Custom navigation stack? We gotchu on that too.


```kotlin
teaserSunshine.setOnClickListener {
   startActivity(
      Intent(this, DataEx.takeoverInstance())
   )
}
```

***
### **Eligibility**

Not all of your users will be eligible for PhunCoin (see [advertising](#advertising)).  You should check to see if the user is eligible before showing any PhunCoin branding.

```kotlin
DataEx.isEligible(object : DataEx.EligibleListener {
   override fun isEligible(eligible: Boolean) {
      Toast.makeText(
         this@MainActivity,
         if (eligible) {
            "Device is eligible."
         } else {
            "Device is not eligible."
         },
         Toast.LENGTH_SHORT
         ).show()
   }
})
```

***
### **Checking the user's PhunCoin balance**
You may want to display the user's current asset balance as your user accrues digital assets across the blockchain-powered, mobile-first cryptocurrency ecosystem.

When requesting an updated balance we will also return you a current PhunCoin branding image to display alongside the balance.

```kotlin
DataEx.assetManager().balance(object : AssetManager.BalanceListener {
    override fun onSuccess(List<Asset>) {
        // Load the image and display the balance along side it
    }

    override fun onFailure(message: String) {
        // NOOP
    }
})
```

***
<a id="advertising"></a>
## A bit on device identifiers

### Android
Data SDK relies on the device's current [Advertising ID](https://developer.android.com/training/articles/user-data-ids) through Google Play Services.

> The advertising ID is a user-specific, unique, resettable ID for advertising, provided by Google Play services. It gives users better controls and provides developers with a simple, standard system to continue to monetize your apps. It is an anonymous identifier for advertising purposes and enables users to reset their identifier or opt out of interest-based ads within Google Play apps.

If your user resets their Advertising ID they may be required to claim a pending promotional balance in PhunWallet to reconcile any accrued balance that happened with their new Advertising ID.

Additionally, if they have opted out of personalized ads they will not be eligible for PhunCoin and all Data SDK features will be disabled.

While Data SDK adheres to all of the policies outlined by Play Services, it is up to you to adhere to the [policy requirements](https://support.google.com/googleplay/android-developer/answer/9857753) for publishing on Google Play.

***
<a id="class"></a>
## Class Reference Documentation
The [Reference Documentation](https://phunware.github.io/maas-dataex-android-sdk/index.html) has all of the detailed usage information including all the public methods, parameters, and convenience initializers.

***
<a id="attribution"></a>
## Attribution

Data SDK uses the following 3rd party components.

| Component     | Version  | Description   | License  |
| ------------- | -------  |:-------------:| -----:|
| [OkHttp](https://github.com/square/okhttp) |3.10.0| An HTTP & SPDY client for Android and Java applications. | [Apache 2.0]
| [Gson](https://github.com/google/gson)  |3.10.0| Gson is a Java library that can be used to convert Java Objects into their JSON representation. | [Apache 2.0]
| [Picasso](https://github.com/square/picasso) |2.71828| A powerful image downloading and caching library for Android. | [Apache 2.0]
| [Timber](https://github.com/JakeWharton/timber) |4.7.1| A logger with a small, extensible API which provides utility on top of Android's normal Log class. | [Apache 2.0]

***
<a id="privacy"></a>
## Privacy
You understand and consent to Phunware’s Privacy Policy located at www.phunware.com/privacy. If your use of Phunware’s software requires a Privacy Policy of your own, you also agree to include the terms of Phunware’s Privacy Policy in your Privacy Policy to your end users.
***
<a id="terms"></a>
## Terms
Use of this software requires review and acceptance of our terms and conditions for developer use located at http://www.phunware.com/terms/
