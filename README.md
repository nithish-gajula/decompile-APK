# Decompile .apk


#### Procedure to read the Java files
1. Rename the .apk file to a .zip file, then extract it to access the `res/` files.

2. Download `dex2jar` tool from the link https://github.com/pxb1988/dex2jar/releases

3. `dex2jar` needs `java`, so make sure you have Java installed on your system. If not can be installed with `sudo apt install openjdk-17-jdk`

4. Extract the dex2jar zip file and navigate into the directory, then type this command `sh d2j-dex2jar.sh -f ../Chart_Maker_Pro.apk -o ../Chart_Maker_Pro.jar`

5. Once jar file generated, Download `JD-GUI` tool from the link https://java-decompiler.github.io/ and download `jd-gui-1.6.6.deb` file for linux. Then install the tool with linux software installer.

6. Open generated `.jar` file in `JD-GUI` tool, Here you're able to see the `java code`, But not images, drawables, etc..

#### Procedure to read the res/ files

7. To see then we need `Apktool`, Follow the procedure from the link https://apktool.org/docs/install/ to setup the apktool and framework-res.apk file

8. Navigate to apktool setup directory and type this command `apktool if framework-res.apk`, It should show result something like this `Framework installed to: /root/.local/share/apktool/framework/1.apk`.

9. Now copy Chart_Maker_Pro.apk into apktool setup directory and type this command `apktool d Chart_Maker_Pro.apk -o Chart_Maker_Pro_Dir` it will generate the readable directory. `d` in command refers to decompile.

10. Tip : Some directories and files ownership for root user only, you can change it by `chown -R icps1101:icps1101 /home/icps1101/Downloads/decompile_apks/Apktool_new` command. It will change the entire directory ownership to specific user. `-R` in command refers to recurssivly. 

#### Additional tools and Procedures

11. **AXML Parser** : This tool is just to show some basic information about the application. Follow the link https://github.com/appknox/pyaxmlparser/releases/tag/v0.3.31 to download the tool and install the requiremnets using `pip install .` command within that directory. Make sure `python` installed in your system before trying. Then you can type `apkinfo Chart_Maker_Pro.apk` to see the informtion.

12. **NinjaDroid** : This tool uses AXML Parser and shows much more information about the application. Follow the link https://github.com/rovellipaolo/NinjaDroid/tags to download the tool, make sure python is installed in your system and type these commands one by one `make build-linux` --> `make install` --> `ninjadroid --help`. Then you can see the app info `ninjadroid ../Chart_Maker_Pro.apk`. Best part is, you can use `ninjadroid Chart_Maker_Pro.apk --all --extract` command to extract the `res/` info without using `AXML Parser`.

13. Alternate to _step 4_ you can also try `sh d2j-dex2jar.sh ../Chart_Maker_Pro_Dir/classes.dex` command to generate the jar file within the same directory and can be opened with JD-JUI application.

14. Without installing any tools, You can also try http://www.javadecompilers.com/ site and upload your apk file to get the jar and class files, But only works when `ad-blocker` disabled.

15. There is a Android application named `show java - a java decompiler` in playstore. Can give a try.

16.  **Analyze APK** : Android studio providing a feature to analyze the apk. Follow `Build -> Analyze APK -> select apk`. It will not show the decompiled code.

17. **Profile or Debug APK** : Android studio also providing a feature to debug the apk. Close all opened projects, then click on `profile or debug apk` and select the apk file. It will also not show the decompiled code.

18. Alternate to _step_2_ you can download the `jadx` tool from the link https://github.com/skylot/jadx/releases/tag/v1.5.2 and navigate to bin directory there you can see jadx-gui. You can run this by `./jadx-gui` command.

19. **ApkStudio** : This tool uses `Java`, `Apktool`, `Jadx`, `ADB`, `Uber APK Signer` to visualize the decomiled apk. Download the tool from the link https://github.com/vaibhavpandeyvpz/apkstudio/releases to download the `.AppImage` file and give `+x` execution permissions to it. Then you can open application with `./ApkStudio-x.x.x`.  You need to configure all the paths in the `apkstudio --> Edit --> Settings --> Binaries`. **examples** Java : `/usr/lib/jvm/java-17-openjdk-amd64/bin/java`, Apktool : `/home/icps1101/Downloads/decompile_apks/Apktool/apktool.jar`, Jadx : `/home/icps1101/Downloads/decompile_apks/jadx-1.5.2/bin/`, ADB : `/usr/local/bin/`, Uber APK Signer : `/home/icps1101/Downloads/decompile_apks/ApkStudio-5.2.4-x64/`. Uber APK Signer can be downloaded from the link https://github.com/patrickfav/uber-apk-signer/releases as a jar file. Now you can open the apk file, but this tool takes time in loading files just give it a minute it will work.

20. For reference ```root@icps1101:/usr/local/bin# ls
`adb  apkinfo  apktool  apktool.jar  coverage  coverage3  coverage-3.10  epylint  isort  isort-identify-imports  ninjadroid  pylint  pyreverse  symilar`
root@icps1101:/usr/local/bin# ``` are available in my system after everything I've setup.

21. **APK Editor Studio** : This tool comes with `apktool, adb, apk signer, zip aligner, framework` Internally, and you just need select an apk file to open, It will show smali code instead of java code. Follow the link https://qwertycube.com/apk-editor-studio/download/ to download the `.AppImage` file and give `+x` execution permissions to it. Then you can open application with `./Apk-editor-Studio`.

22. Tip : You can see the java code (not pure) from the `jd-gui` or `jadx-gui` and smali code from the `Apk Editor Studio`. Then you compare them both for conneting dots to understand the actual code logic.


## some information

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
