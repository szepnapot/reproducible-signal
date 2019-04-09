# reproducible-signal

Reproducible SignalApp build from source, signed with own key 

To add to rattlesnake config include the following:

```yaml
[[custom-prebuilts]]
  modules = ["signal"]
  repo = "https://github.com/szepnapot/reproducible-signal"
```

# Build SignalApp from source

```bash
# Clone the Signal Android source repository
git clone https://github.com/signalapp/Signal-Android.git && cd Signal-Android

# Check out the release tag for the version you'd like to compare
git checkout v[the version number]

# Build using the Docker environment
docker run --rm -v $(pwd):/project -w /project whispersystems/signal-android:1.3 ./gradlew clean assembleRelease
```

The built (no-signed) apks can be found in `build/outputs/apk/play/release/`.

# Sign APK(s)

Download [uber-apk-signer](https://github.com/patrickfav/uber-apk-signer)

```bash
java -jar uber-apk-signer-1.0.0.jar --apks build/outputs/apk/play/release/ -o /home/ubuntu/signal-build/signed_apks --ks [keystore] --ksAlias [alias] --ksKeyPass [pass] --ksPass [pass]
```
