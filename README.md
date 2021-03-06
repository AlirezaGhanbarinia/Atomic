# Atomic
 [ ![Download](https://api.bintray.com/packages/infideap2/Atomic/Atomic/images/download.svg) ](https://bintray.com/infideap2/Atomic/Atomic/_latestVersion)

An android restful api/networking library using okhttp library as backbone.

Android 9.0+ support

## Including In Your Project
If you are a Maven user you can easily include the library by specifying it as
a dependency:

#### Maven
``` xml
<dependency>
  <groupId>com.infideap.atomic</groupId>
  <artifactId>atomic</artifactId>
  <version>0.0.3</version>
  <type>pom</type>
</dependency>
```
#### Gradle
```groovy
dependencies {
   compile 'com.infideap.atomic:atomic:0.0.3'
}
```

if **the gradle unable to sync**, you may include this line in project level gradle,
```groovy
repositories {
 maven{
   url "https://dl.bintray.com/infideap2/Atomic/"
 }
}
```

**or**,
you can include it by **download this project** and **import /atomic** as **module**.

## How to use

**POST**
```java
Atom.with(LoginActivity.this)
    .load("https://reqres.in/api/login")
    .setJsonPojoBody(loginRequest)
    .as(LoginResponse.class)
    .setCallback(new FutureCallback<LoginResponse>() {
        @Override
        public void onCompleted(Exception e, LoginResponse result) {
            if (e != null) {
                e.printStackTrace();
            } else if (result.token != null) {
                Snackbar.make(v, "Pass : " + result.token, Snackbar.LENGTH_LONG).show();
            } else if (result.error != null) {
                Snackbar.make(v, "Fail : " + result.error, Snackbar.LENGTH_LONG).show();
            }
        }
    });
```

**GET**
```java
Atom.with(LoginActivity.this)
    .load("https://reqres.in/api/users/2")
    .as(UserResponse.class)
    .setCallback(new FutureCallback<LoginResponse>() {
        @Override
        public void onCompleted(Exception e, UserResponse result) {
            if (e != null) {
                e.printStackTrace();
            } else if (result.first_name != null) {
                Snackbar.make(v, "Pass : " + result.first_name, Snackbar.LENGTH_LONG).show();
            } 
        }
    });
```

**Other**, just add method after url on load()
```java
Atom.with(LoginActivity.this)
    .load("https://reqres.in/api/users/2", Atom.DELETE_METHOD)
    .asString()
    .setCallback(new FutureCallback<String>() {
        @Override
        public void onCompleted(Exception e, String result) {
            if (e != null) {
                e.printStackTrace();
            } else if (result != null) {
                Snackbar.make(v, "Pass : " + result, Snackbar.LENGTH_LONG).show();
            } 
        }
    });
```

**Upload File**
```java
Atom.with(LoginActivity.this)
    .load("https://reqres.in/api/user/2")
    .setJsonPojoBody(userRequest)
    .setMultipartFile("uploadFile", new File("video.mp4"))
    //Optional: Upload Progress
    .uploadProgress(new ProgressCallback() {
        @Override
        public void onProgress(long uploaded, long total) {
            
        }
    })
    .as(UserResponse.class)
    .setCallback(new FutureCallback<UserResponse>() {
        @Override
        public void onCompleted(Exception e, UserResponse result) {
            if (e != null) {
                e.printStackTrace();
            } 
        }
    });
```

**Download File**
```java
Atom.with(LoginActivity.this)
    .load("https://developer.android.com/_static/66ebbcad58/images/android/touchicon-180.png")
    //Optional: Progress
    .progress(new ProgressCallback() {
        @Override
        public void onProgress(long downloaded, long total) {
            
        }
    })
    .write(new File("android.png"))
    .setCallback(new FutureCallback<File>() {
        @Override
        public void onCompleted(Exception e, File result) {
            
        }
    });
```

## Advance
**Customize**
```java
OkHttpClient client =new OkHttpClient.Builder().addInterceptor(new Interceptor() {
    @Override
    public Response intercept(Chain chain) throws IOException {
        return null;
    }
}).build();
Atom.setClient(client);
```

## Contact
For any enquiries, please send an email to tr32010@gmail.com. 

## License

    Copyright 2016-2017 Shiburagi

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
