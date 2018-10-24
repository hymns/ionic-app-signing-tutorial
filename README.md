# ionic-app-signing-tutorial
Step by step guide to signing your ionic application

# Create Store Key
If you does't have keystore yet, you need generate one. Replace <appname> with your own app name.
```
keytool -genkey -v -keystore <appname>-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias <appname>
keytool -importkeystore -srckeystore <appname>-release-key.jks -destkeystore <appname>-release-key.jks -deststoretype pkcs12
```

# Build Release Version
You need build your ionic app on production or release version
```
ionic cordova build android --prod --release
```
Copy the apk builded to specific folder your want.


# Byte Alignment
Before do the signing, we need to align apk package first
```
zipalign -v -p 4 app-release-unsigned.apk app-release-unsigned-aligned.apk
```

# Signed with Private Key
Once completed the zipalign process, now we can sign the apk
```
apksigner sign --ks <appname>-release-key.jks --out <appname>-app-release.apk app-release-unsigned-aligned.apk
```

# Verify Signed App
To make sure your app are sucessfully signed, you can verify the signed package using command below
```
apksigner verify <appname>-app-release.apk
```
