[Gradle Android so 文件过滤插件](https://github.com/Jween/android-soexcluder)
============================

此插件可以根据 buildType 或者 flavor 来过滤 so 文件


使用
-----

1. 在 build.gradle 中添加以下脚本

    ```groovy
    buildscript {
       repositories {
          jcenter()
       }

       dependencies {
          classpath 'com.jween.gradle:android-soexcluder:1.1'
       }
    }


    apply plugin: 'com.android.application'
    apply plugin: 'android-soexcluder'
    ```
    **注意**: `android-soexcluder`插件必须和`com.android.application`插件配合使用


配置
----

1. 根据flavor移除指定so文件

    ```groovy
    soexcluder {
        // 为flavor1 移除v7a的foo.so与v8a的bar.so文件
        flavor1 {
            exclude "lib/armeabi-v7a/foo.so", "lib/armeabi-v8a/bar.so"
        }
        
        // 对debug buildType保留v7a和x86 abi的除foo.so之外的所有so文件
        debug {
            include "lib/armeabi-v7a/*.so" 
            include "lib/x86/*.so"
            exclude "lib/armeabi-v7a/foo.so"
            exclude "lib/x86/foo.so"
        }
    }
    ```

2. 与 gradle 的 include/exclude 的Ant路径正则用法完全一致

    ```groovy
    soexcluder {
        
        // 对debug buildType保留除foo.so之外的所有so文件
        debug {
            include "**/*" 
            exclude "**/foo.so"
        }
    }
    ```

3. 你甚至可以对buildType以及flavor使用正则表达式!
 
     ```groovy
     soexcluder {
         
         // 当flavor或者buildType的名字以o结尾的时候, 移除所有so文件
         ".*o" {
             exclude "**/*"
         }
     }
     ```

License   
-------   
 
    "THE BEER-WARE LICENSE" (Revision 42):

    <Jween.Lau@gmail.com> wrote this file. As long as you retain this notice
    you can do whatever you want with this stuff. If we meet some day, and you think
    this stuff is worth it, you can buy me a beer in return. -Jween Lau
 

[Anti-996 License](https://github.com/996icu/996.ICU/blob/master/LICENSE)
--------
 
 - The purpose of this license is to prevent anti-labour-law companies from using the software or codes under the license, and force those companies to weigh their way of working
 - See a [full list of projects](https://github.com/996icu/996.ICU/blob/master/awesomelist/README.md) under Anti-996 License
 
 - This draft is adapted from the MIT license. For more detailed explanation, please see [Wiki](https://github.com/kattgu7/996-License-Draft/wiki). This license is designed to be compatible with all major open source licenses.  
 - For law professionals or anyone who is willing to contribute to future version directly, please go to [Anti-996-License-1.0](https://github.com/kattgu7/996-License-Draft). Thank you.