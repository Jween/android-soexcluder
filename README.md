[Gradle Android So Excluder Plugin](https://github.com/Jween/android-soexcluder)
=========================================

This plugin will help you exclude so files by flavor or buildType   

[中文版本 README](README.cn.md)


Usage
-----

1. Add the following scripts to your build.gradle

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
    **Note**: You MUST apply `android-soexcluder` along with `com.android.application`   

2. Wish we have step 2! 
 
    But that's it, it a quite simple small tool to deal with so files.

Configuration
-------------

1. Exclude specific so files by flavors

    ```groovy
    soexcluder {
        // exclude armeabi-v7a/foo.so and armeabi-v8a/bar.so for flavor1
        flavor1 {
            exclude "lib/armeabi-v7a/foo.so", "lib/armeabi-v8a/bar.so"
        }
        
        // Reserve only v7a and x86 so files except foo.so for debug buildType
        debug {
            include "lib/armeabi-v7a/*.so" 
            include "lib/x86/*.so"
            exclude "lib/armeabi-v7a/foo.so"
            exclude "lib/x86/foo.so"
        }
    }
    ```

2. Exact the same path pattern as gradle include/exclude api

    ```groovy
    soexcluder {
        
        // Reserve all so files for debug buildType except foo.so
        debug {
            include "**/*" 
            exclude "**/foo.so"
        }
    }
    ```

3. You can even use regex in flavor/buildType entry!
 
     ```groovy
     soexcluder {
         
         // Remove all so files if the flavor or buildType name ends with 'o' 
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