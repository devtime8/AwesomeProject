

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


![img_18.png](img_18.png)

![img_19.png](img_19.png)

![img_20.png](img_20.png)


![img_21.png](img_21.png)

![img_22.png](img_22.png)


![img_23.png](img_23.png)



### 내부 테스트 버전 만들기  - 패키지 문제 해결 후 다시 ㅠㅠㅠ 언제 앱출시 테스트 해보냐????

![img_24.png](img_24.png)


![img_25.png](img_25.png)


![img_26.png](img_26.png)



![img_28.png](img_28.png)

![img_27.png](img_27.png)


![img_29.png](img_29.png)




### Generating the release AAB

    App Bundle


![img_30.png](img_30.png)


![img_31.png](img_31.png)

![img_32.png](img_32.png)

    npx react-native build-android --mode=release

![img_33.png](img_33.png)


![img_34.png](img_34.png)


### app-release.aab  파일을 드래그 

![img_36.png](img_36.png)
![img_35.png](img_35.png)


### 성공  - app-release.aab  업로드 하기 힘들다...

![img_37.png](img_37.png)



### 또 뭐고????????????
![img_38.png](img_38.png)





### 경고 1개 패스 모르겠당...................

    내부 테스트 버전 만들기
    버전에 문제가 있습니다.
    새 버전 출시하기
    2
    미리보기 및 확인
        오류, 경고 및 메시지
        경고 1개
            버전 코드 2 메시지 1개
            경고
                이 App Bundle 유형과 연결된 가독화 파일이 없습니다. 
                난독화된 코드(R8/proguard)를 사용하는 경우 가독화 파일을 업로드하면 비정상 종료 및 ANR을 더 쉽게 분석하고 디버그할 수 있습니다.
                R8/proguard를 사용하면 앱 크기를 줄이는 데 도움이 됩니다. 자세히 알아보기



![img_39.png](img_39.png)


![img_40.png](img_40.png)



![img_41.png](img_41.png)



### 출시
    2 (1.0)
        내부 테스터에게 제공됨
            버전 코드 1개
                게시일: 3월 2일 오후 12:56
                    검토되지 않음


![img_42.png](img_42.png)



![img_43.png](img_43.png)

![img_44.png](img_44.png)



### www index.html 업데이트


![img_45.png](img_45.png)


