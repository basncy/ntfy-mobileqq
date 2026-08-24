# Steps to Build as mobileqq

#### patch
```
sed -e '/com.google.gms.google-services/d' \
    -e 's/applicationId "io.heckel.ntfy"/applicationId "com.tencent.mobileqq"/g' \
    -e 's/variant ->//g' \
    -e '/def shouldProcessGoogleServices/d' \
    -e '/def googleTask/d' \
    -e '/googleTask.enabled/d' \
     -i app/build.gradle
sed -e 's/io.heckel.ntfy.SEND_MESSAGE/com.tencent.mobileqq.SEND_MESSAGE/g' -i app/src/main/AndroidManifest.xml
sed -e '/com.google.gms:google-services/d' -i build.gradle
```
#### build
#Deprecatred ./gradlew build
在 Android Studio 左下角打开 Build Variants 面板，将你的模块切换为 release。
在顶部菜单栏点击 Build -> Build Bundle(s) / APK(s) -> Build APK(s)
ls app/build/outputs/apk/fdroid/release/

### genkeys（One-time only）
```
keytool -genkey -v -keystore my-key.keystore -alias my-alias -keyalg RSA -keysize 2048 -validity 10000
```
### sign
```
zipalign -v 4 app/build/outputs/apk/fdroid/release/app-fdroid-release-unsigned.apk app/build/outputs/apk/fdroid/release/app-fdroid-release-aligned.apk
apksigner sign --ks my-key.keystore --out app/build/outputs/apk/fdroid/release/app-fdroid-release-signed.apk app/build/outputs/apk/fdroid/release/app-fdroid-release-aligned.apk
ls app/build/outputs/apk/fdroid/release/app-fdroid-release-signed.apk
```
============================================================================================================================

# ntfy Android App

This is the Android app for [ntfy](https://github.com/binwiederhier/ntfy) ([ntfy.sh](https://ntfy.sh)). You can find the app in [F-Droid](https://f-droid.org/packages/io.heckel.ntfy/) or the [Play Store](https://play.google.com/store/apps/details?id=io.heckel.ntfy), 
or as .apk files on the [GitHub releases page](https://github.com/binwiederhier/ntfy-android/releases).

If you're downloading the APKs from GitHub, they are signed with a certificate with the following SHA-256 fingerprint: `6e145d7ae685eff75468e5067e03a6c3645453343e4e181dac8b6b17ff67489d`. You can also query the DNS TXT records for `ntfy.sh` to find this fingerprint.

## Build
For up-to-date building instructions, please see the [official docs](https://docs.ntfy.sh/develop/#android-app).

## Translations
We're using [Weblate](https://hosted.weblate.org/projects/ntfy/) to translate the ntfy Android app. We'd love your participation.

<a href="https://hosted.weblate.org/engage/ntfy/">
<img src="https://hosted.weblate.org/widgets/ntfy/-/multi-blue.svg" alt="Translation status" />
</a>

## License
Made with ❤️ by [Philipp C. Heckel](https://heckel.io), distributed under the [Apache License 2.0](LICENSE).

Thank you to these fantastic resources:
* [RecyclerViewKotlin](https://github.com/android/views-widgets-samples/tree/main/RecyclerViewKotlin) (Apache 2.0)
* [Just another Hacker News Android client](https://github.com/manoamaro/another-hacker-news-client) (MIT)
* [Android Room with a View](https://github.com/googlecodelabs/android-room-with-a-view/tree/kotlin) (Apache 2.0)
* [Firebase Messaging Example](https://github.com/firebase/quickstart-android/blob/7147f60451b3eeaaa05fc31208ffb67e2df73c3c/messaging/app/src/main/java/com/google/firebase/quickstart/fcm/kotlin/MyFirebaseMessagingService.kt) (Apache 2.0)
* [Designing a logo with Inkscape](https://www.youtube.com/watch?v=r2Kv61cd2P4)
* [Foreground service](https://robertohuertas.com/2019/06/29/android_foreground_services/)
* [github/gemoji](https://github.com/github/gemoji) (MIT) for as data source for an up-to-date [emoji.json](https://raw.githubusercontent.com/github/gemoji/master/db/emoji.json) file
* [emoji-java](https://github.com/vdurmont/emoji-java) (MIT) has been stripped and inlined to use the emoji.json file
