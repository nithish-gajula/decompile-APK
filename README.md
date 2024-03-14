# decompile-APK
This repository tells you what is and how to decompile the APK to it's maximum.

While writing the code for your Android app, there may be some lines of code that are unnecessary and may increase the size of your app’s APK. Aside from useless code, there are numerous libraries that you may have incorporated in your program but did not use all of the functionalities that each library provides. Also, you may have developed some code that will be obsolete in the future and failed to delete it. These factors are to blame for the increased size of your application’s APK. Android has Proguard capability to minimize the size of the APK. ProGuard is a free Java app for Android that allows us to do the following:

1. Reduce (minimize) the code: Unused code in the project should be removed.
2. Code obfuscation: Rename the names of classes, fields, and so on.
3. Improve the code: Inline the functions, for example.

In summary, ProGuard has the following effect on our project:

* It shrinks the application’s size.
* It removes unused classes and methods that contribute to an Android application’s 64K method count limit.
* By obfuscating the code, it makes it difficult to reverse engineer the application.

Proguard is included by default in Android Studio and can help in a variety of ways, a few of which are listed below.

- It obfuscates the code, which means that it changes the names to something smaller, such as A for MainViewModel. After obfuscating the app, reverse engineering becomes difficult.
- It shrinks the resources, ignoring resources that are not called by our Class files, are not used in our Android app, such as images from drawable, and so on. This will significantly reduce the app’s size. To keep your app light and fast, you should always shrink it.