# Android Concepts

## Android System Architecture（Android 系统架构）
Four architecture layers: **Linux layer**, **system run-time library layer**, **application framework layer** and **application layer**.

### 1. Linux Layer（Linux 内核层）
Android system is based on Linux kernel. This layer provides hardware of an Android device, such as display driver, audio driver, camera driver, bluetooth driver, Wi-Fi driver, battery management, etc.

### 2. System Run-time Library Layer（系统运行层）
This layer achieved most characteristics of Android system by importing some C/C++ libraries. For instance, SQLite library, OpenGl/ES library, Webkit library, etc.

Run-time Library provides some core library for Android system. These libraries allow developer write Android application by using Java language. Additionally, Android Run-time Library involved a Dalvik virtual machine as well, it allows Android application to run on a independent thread and have its own Dalvik virtual machine instance.

### 3. Application Framework Layer（应用框架层）
This layer provides some APIs which you probably want to use it when you build your application.

### 4. Application Layer（应用层）
Apps on your phone including "Contect", "Messager" are all belong to this layer.

