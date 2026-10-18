information needed.

# ## iOS

iOS uses several different dependency management systems. One of the more common systems is CocoaPods. If you open the iOSApp/Podfile file, you’ll see there isn’t much to it:

```
```
target 'iosApp' do
  use_frameworks!
  platform :ios, '14.1'
  pod 'shared', :path => '..//shared'
end
```
```

The most important part is the `pod 'shared', :path => '..//shared'` section. This defines the shared framework that KMP will create and that you can use in your iOS apps.

# ## BuildSrc

One of the nice features of the newer Gradle versions is the concept of the buildSrc module. This is a module where you can define version variables as well as define your own plugins. To create this module, start by right-clicking the root folder in the project view. Then, select New ▶ Directory. Enter buildSrc. Since this will be a module, you’ll need a build file. Right-click buildSrc and choose New ▶ File. Name the file build.gradle.kts and add the following code to it:

```
```
repositories {
  mavenCentral()
}

plugins {
  'kotlin-dsl'
}
```
```

The code above includes the Kotlin DSL plugin. Now, sync your Gradle files by clicking Sync Now at the top right corner of the window. Then, right-click buildSrc, select New ▶ Directory and choose src/main/kotlin. Right-click the kotlin directory and select New ▶ Kotlin Class/File. Name the file Dependencies and choose File. This file will contain all the variables you’ll need to define all your plugins and dependencies. The reason for creating this file is to avoid having to maintain all the versions for your plugins and dependencies in many different files. Defining the versions in one place makes it easy to change later.