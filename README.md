# phonegap-plugin-push [![Build Status](https://travis-ci.org/phonegap/phonegap-plugin-push.svg)](https://travis-ci.org/phonegap/phonegap-plugin-push)

> Register and receive push notifications

# 1.x에서 2.x로 업데이트할때의 팁

기본적으로 1.x에서 2.x로 플러그인을 새로 설치하고 빌드를 진행하면 로그에서 parsing google-services.json에 대한 로그가 나와야 정상이나 그렇지 않을 때가 있습니다.

아래의 순서에 따라 그레이들에 지정된 버전을 고친뒤 시도합니다.

**시험환경**
```bash
ionic 1.7.14
cordova 7.1.1
cordova-android 6.2.1
phonegap-plugin-push 1.6.2 -> 2.0.0
```

1. platforms > android > phonegap-plugin-push/XXXXXXX-push.gradle을 엽니다.  
2. classpath 'com.google.gms:google-services:3.0.0' 과 apply plugin: com.google.gms.googleservices.GoogleServicesPlugin 을 삭제  
3. platforms > android > build.gradle 의 34행부근에 classpath 'com.google.gms:google-services:3.2.1' 를 추가  
4. build.gradle 의 마지막에 apply plugin: 'com.google.gms.google-services' 를 추가  
5. (Build중 Firebase에 에러가 나온다면) platforms > android > project.properties 의 cordova.system.library.5=com.google.firebase:firebase-messaging:11.0.1 를11.0.4 지정한다.  
6. ionic build android 문제없이 빌드되며 파싱로그도 확인가능, FCM콘솔에서 기기가 등록된것을 알 수 있었다.

# What is this?

This plugin offers support to receive and handle native push notifications with
a **single unified API**.

This does not mean you will be able to send a single push message and have it
arrive on devices running different operating systems. By default Android uses
FCM and iOS uses APNS and their payloads are significantly different. Even if
you are using FCM for both Android and iOS there are differences in the payload
required for the plugin to work correctly. For Android **always** put your push
payload in the `data` section of the push notification. For more information on
why that is the case read
[Notification vs Data Payload](https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/PAYLOAD.md#notification-vs-data-payloads).
For iOS follow the regular
[FCM documentation](https://firebase.google.com/docs/cloud-messaging/http-server-ref).

This plugin does not provide a way to determine which platform you are running
on. The best way to do that is use the `device.platform` property provided by
[cordova-plugin-device](https://github.com/apache/cordova-plugin-device).

Starting with version `2.0.0`, this plugin will support `CocoaPods` installation
of the `Firebase Cloud Messaging` library. More details are available in the
[Installation](docs/INSTALLATION.md#cocoapods) documentation.

* [Reporting Issues](docs/ISSUES.md)
* [Installation](docs/INSTALLATION.md)
* [API reference](docs/API.md)
* [Typescript support](docs/TYPESCRIPT.md)
* [Examples](docs/EXAMPLES.md)
* [Platform support](docs/PLATFORM_SUPPORT.md)
* [Cloud build support (PG Build, IntelXDK)](docs/PHONEGAP_BUILD.md)
* [Push notification payload details](docs/PAYLOAD.md)
* [Contributing](.github/CONTRIBUTING.md)
* [License (MIT)](MIT-LICENSE)