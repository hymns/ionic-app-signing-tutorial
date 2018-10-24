# Ionic App Signing Tutorial
Step by step guide to signing your ionic application

### Create Store Key
If you doesn't have keystore yet, you need to generate it first. Replace &lt;appname&gt; with your own app name.
```
keytool -genkey -v -keystore <appname>-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias <appname>
keytool -importkeystore -srckeystore <appname>-release-key.jks -destkeystore <appname>-release-key.jks -deststoretype pkcs12
```

### Build Release Version
You need build your ionic app for production or release version
```
ionic cordova build android --prod --release
```
After build completed, copy the apk to specific folder your want for the next process.


### Byte Alignment
Before do the signing process, we need to align apk package first
```
zipalign -v -p 4 app-release-unsigned.apk app-release-unsigned-aligned.apk
```

### Signed with Private Key
Once finished the zipalign process, now we ready to signing the apk for release
```
apksigner sign --ks <appname>-release-key.jks --out <appname>-app-release.apk app-release-unsigned-aligned.apk
```

### Verify Signed App
To make sure your app are sucessfully signed, you can verify the signed app using command below
```
apksigner verify <appname>-app-release.apk
```
