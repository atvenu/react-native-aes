# React Native AES

AES encryption/decryption for react-native

## Installation
```sh
npm install --save react-native-aes-crypto
```
### Installation (iOS)
* See [Linking Libraries](http://facebook.github.io/react-native/docs/linking-libraries-ios.html)
OR
* Drag RCTAes.xcodeproj to your project on Xcode.
* Click on your main project file (the one that represents the .xcodeproj) select Build Phases and drag libRCTAes.a from the Products folder inside the RCTAes.xcodeproj.

### Installation (Android)
#### Untested!
```gradle
...
include ':react-native-aes'
project(':react-native-aes').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-aes/android/RCTAes')
```

* In `android/app/build.gradle`

```gradle
...
dependencies {
    ...
    compile project(':react-native-aes')
}
```

* register module (in MainApplication.java)

```java
......
import com.tectiv3.aes.RCTAesPackage;

......

@Override
protected List<ReactPackage> getPackages() {
   ......
   new RCTAesPackage(),
   ......
}
```

## Usage

### Example

```js
import { NativeModules } from 'react-native';
var Aes = NativeModules.Aes;

Aes.generateKey("Arnold", function(key) {
    console.log(key);
    Aes.encrypt("These violent delights have violent ends", key, function(base64) {
        console.log(base64);
        Aes.decrypt(base64, key, function(text) {
            console.log(text);
        }, function(){
            console.log("decrypt error");
        });
    }, function() {
        console.log("encrypt error");
    });
}, function() {
    console.log("generate key error");
});
```

### methods

- `encrypt(text, key, callback)`
- `decrypt(base64, key, callback)`
- `generateKey(text, callback)`
