# 将Flutter添加进已存在的App

## 介绍

### 接入现有App(Add-to-app)

*Add-to-app为一个整体单词，其意大概为"将Flutter嵌入到App里"以下简称"接入现有App"*

直接使用Flutter重写整个应用程序有时是不切实际的。对于这种情况，Flutter也可以作为库或者模块集成于应用程序中。这个模块可以导入到您的Android或iOS（当前支持的平台）项目中，以在Flutter中呈现您应用程序的一部分UI。或者只是用来执行Dart代码实现的逻辑。

只需几步，您就可以将Flutter的生产力和表现力引入到自己的应用程序中。

从Flutter v1.12开始，**接入现有App**(Add-to-app)提供给App的方案是，每个应用在同一时间可以集成一个全屏幕的 Flutter 实例。它目前有**以下局限性**：

* 运行多个Flutter实例或在部分屏幕视图中运行可能会有不可预知的行为。
* 在后台模式下使用Flutter还在开发中。
* 不支持将多个Flutter库打包到同一个应用程序中。
* 在Android上的**接入现有App**(Add-to-app)中使用的插件，需要基于Fluttle插件使用基于`FlutterPlugin`的新Android插件API*（旧的Flutter插件基于`PluginRegistry.Registrar`，从1.12开始新的插件API使用基于`FlutterPlugin`）*。如果使用不支持`FluttlePlugin`的插件在**接入现有App**(Add-to-app)中可能会有不可预知的行为（比如认为 Flutter `Activity` 一直处于活跃状态）。
* 从v1.17开始，Flutter模块只支持AndroidX应用程序。

### 支持的特性

#### 添加到Android应用中

![1](/images/add_flutter_to_existing_app/add_flutter_to_existing_app_1.gif)

- 在 Gradle 脚本中添加一个Flutter SDK语句即可自动构建并引入 Flutter 模块。
- 将 Flutter 模块构建为通用的 `Android Archive (AAR)` 以便集成到您自己的构建系统中，并提高 Jetifier 与 AndroidX 的互操作性；
- `FlutterEngine` API 用于启动并持续地为挂载 `FlutterActivity`或`FlutterFragment` 提供独立的 Flutter 环境；
- Android Studio 的 Android/Flutter 协同编辑，以及 Flutter module 创建与导入向导；
- 支持 Java 和 Kotlin 为宿主的应用程序；
- Flutter 模块可以通过使用 `Flutter plugins` 与平台进行交互。 Android 平台的 plugin 应该`迁移至 V2 plugin API`以确保最佳的兼容性。在 Flutter v1.12，大多数 `Flutter 团队维护`的 plugin，以及`FlutterFire` 都已完成迁移；
- 支持通过从 IDE 或命令行中使用 `flutter attach` 来实现 Flutter 调试与有状态的热重载。

#### 添加到iOS应用中

- 使用CocoaPods添加Flutter SDK语句即可自动构建并引入Flutter模块到Xcode的Build Phase中

- 将 Flutter 模块构建为通用的 [iOS Framework](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPFrameworks/Concepts/WhatAreFrameworks.html) 以便集成到您自己的构建系统中

- `FlutterEngine` API 用于启动并持续地为挂载`FlutterViewController`以提供独立的 Flutter 环境；

- 支持 Objective-C 和 Swift 为宿主的应用程序；

- Flutter 模块可以通过使用 `Flutter plugins`与平台进行交互；

- 支持通过从 IDE 或命令行中使用 `flutter attach` 来实现 Flutter 调试与有状态的热重载。

  查看 [add-to-app GitHub 示例仓库](https://github.com/flutter/samples/tree/master/experimental/add_to_app) 中在 iOS 和 Android 平台上引入 Flutter module 的示例项目。
  
  

## 添加到Android应用中

