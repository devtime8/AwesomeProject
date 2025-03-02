

# https://reactnative.dev/docs/signed-apk-android

# https://reactnative.dev/docs/signed-apk-android#windows

## Generating an upload key


    keytool -genkeypair -v -storetype PKCS12 -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000


        my-upload-key.keystore


![img_4.png](img_4.png)

![img_5.png](img_5.png)

![img_6.png](img_6.png)




### caution
    my-upload-key.keystore

    Remember to keep the keystore file private. In case you've lost upload key or it's been compromised you should follow these instructions.
    



## Setting up Gradle variables
    
    Place the my-upload-key.keystore file under the android/app directory in your project folder.
    Edit the file ~/.gradle/gradle.properties or android/gradle.properties, 
    and add the following 
    (replace ***** with the correct keystore password, 
    alias and key password),
        
        MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore
        MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
        MYAPP_UPLOAD_STORE_PASSWORD=*****
        MYAPP_UPLOAD_KEY_PASSWORD=*****

    
    Note about using git
    Saving the above Gradle variables in ~/.gradle/gradle.properties 
    instead of android/gradle.properties 
    prevents them from being checked in to git. 
    You may have to create the ~/.gradle/gradle.properties file 
    in your user's home directory 
    before you can add the variables.
    

![img_7.png](img_7.png)


### Adding signing config to your app's Gradle config
    android/app/build.gradle

        ...
        android {
            ...
            defaultConfig { ... }
            signingConfigs {
                release {
                    if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')) {
                        storeFile file(MYAPP_UPLOAD_STORE_FILE)
                        storePassword MYAPP_UPLOAD_STORE_PASSWORD
                        keyAlias MYAPP_UPLOAD_KEY_ALIAS
                        keyPassword MYAPP_UPLOAD_KEY_PASSWORD
                    }
                }
            }
            buildTypes {
                release {
                    ...
                    signingConfig signingConfigs.release
                }
            }
        }
        ...

![img_11.png](img_11.png)









### Generating the release AAB


    npx react-native build-android --mode=release

![img_8.png](img_8.png)

    C:\dev9\android\AwesomeProject\android\app\build\outputs\bundle\release
    app-release.aab


    ![img_9.png](img_9.png)


    ![img_10.png](img_10.png)



### Testing the release build of your app

    1. delete app in phone
    2. npm run android -- --mode="release"

    Before uploading the release build to the Play Store, 
    make sure you test it thoroughly. 
    First uninstall any previous version of the app you already have installed.
    Install it on the device using the following command in the project root:
        
        npm run android -- --mode="release"


![img_12.png](img_12.png)

![img_13.png](img_13.png)

![img_14.png](img_14.png)


### 'com.awesomeproject'은(는) 이미 Google Play에 존재하므로 다른 패키지 이름을 사용해야 합니다.



![img_15.png](img_15.png)



![](assets/2025-03-02-11-45-52.png)


![](assets/2025-03-02-11-46-10.png)


![](assets/2025-03-02-11-46-24.png)


![](assets/2025-03-02-11-50-36.png)



![](assets/2025-03-02-11-51-36.png)



![](assets/2025-03-02-11-51-56.png)


![img_16.png](img_16.png)


![img_17.png](img_17.png)

