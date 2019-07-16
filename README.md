# flutter_facebook-instagram_share

*** This is a fork from proyect https://github.com/roughike/flutter_facebook_login cleaning proyect in process

A Flutter plugin for using the native Facebook Login SDKs on Android and iOS to share image, iPhoneHooks and AndroidIntents to share with instagram on iOS and Android. and Others (native share image all apps installed)
https://developers.facebook.com/docs/sharing/ios/
https://developers.facebook.com/docs/sharing/android/
https://www.instagram.com/developer/mobile-sharing/


## AndroidX support

* if you want to **avoid AndroidX**, use version 1.2.0.
* for [AndroidX Flutter projects](https://flutter.dev/docs/development/packages-and-plugins/androidx-compatibility), use versions 2.0.0 and up.

## Installation

To get things up and running, you'll have to declare a pubspec dependency in your Flutter project.
Also some minimal Android & iOS specific configuration must be done, otherise your app will crash.

### On your Flutter project

See the [installation instructions on pub](https://pub.dartlang.org/packages/flutter_facebook_login#-installing-tab-).

### Android

This assumes that you've done the _"Associate Your Package Name and Default Class with Your App"_ and
 _"Provide the Development and Release Key Hashes for Your App"_ in the [the Facebook Login documentation for Android site](https://developers.facebook.com/docs/facebook-login/android).

After you've done that, find out what your _Facebook App ID_ is. You can find your Facebook App ID in your Facebook App's dashboard in the Facebook developer console.

Once you have the Facebook App ID figured out, youll have to do two things.

First, copy-paste the following to your strings resource file. If you don't have one, just create it.

**\<your project root\>/android/app/src/main/res/values/strings.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">Your App Name here.</string>

    <!-- Replace "000000000000" with your Facebook App ID here. -->
    <string name="facebook_app_id">000000000000</string>

    <!--
      Replace "000000000000" with your Facebook App ID here.
      **NOTE**: The scheme needs to start with `fb` and then your ID.
    -->
    <string name="fb_login_protocol_scheme">fb000000000000</string>
</resources>
```

Then you'll just have to copy-paste the following to your _Android Manifest_:

**\<your project root\>/android/app/src/main/AndroidManifest.xml**

```xml
<meta-data android:name="com.facebook.sdk.ApplicationId"
    android:value="@string/facebook_app_id"/>

<activity android:name="com.facebook.FacebookActivity"
    android:configChanges=
            "keyboard|keyboardHidden|screenLayout|screenSize|orientation"
    android:label="@string/app_name" />

<activity
    android:name="com.facebook.CustomTabActivity"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="@string/fb_login_protocol_scheme" />
    </intent-filter>
</activity>
```

A sample of a complete AndroidManifest file can be found [here](https://github.com/roughike/flutter_facebook_login/blob/master/example/android/app/src/main/AndroidManifest.xml#L39-L56).

Done!

### iOS

This assumes that you've done the _"Register and Configure Your App with Facebook"_ step in the
[the Facebook Login documentation for iOS site](https://developers.facebook.com/docs/facebook-login/ios).
(**Note**: you can skip "Step 2: Set up Your Development Environment").

After you've done that, find out what your _Facebook App ID_ is. You can find your Facebook App ID in your Facebook App's dashboard in the Facebook developer console.

Once you have the Facebook App ID figured out, then you'll just have to copy-paste the following to your _Info.plist_ file, before the ending `</dict></plist>` tags.

**\<your project root\>/ios/Runner/Info.plist**

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleURLSchemes</key>
        <array>
            <!--
              Replace "000000000000" with your Facebook App ID here.
              **NOTE**: The scheme needs to start with `fb` and then your ID.
            -->
            <string>fb000000000000</string>
        </array>
    </dict>
</array>

<key>FacebookAppID</key>

<!-- Replace "000000000000" with your Facebook App ID here. -->
<string>000000000000</string>
<key>FacebookDisplayName</key>

<!-- Replace "YOUR_APP_NAME" with your Facebook App name. -->
<string>YOUR_APP_NAME</string>

<key>LSApplicationQueriesSchemes</key>
<array>
    <string>fbapi</string>
    <string>fb-messenger-share-api</string>
    <string>fbauth2</string>
    <string>fbshareextension</string>
</array>
```

A sample of a complete Info.plist file can be found [here](https://github.com/cuenca-mx/flutter_facebook_login/blob/master/example/ios/Runner/Info.plist#L57).

Done!

