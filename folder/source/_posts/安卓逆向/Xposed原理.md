---
title: xposed原理
date: 2024-10-14 21:31
---

xposed原理

- zygote进程是android系统第一个java进程，其他所有的apk进程都是通过zygote进程fork的。xposed是一个hook框架，其通过**修改zygote进程**的native层代码和java层代码在zygote进程启动时将xposed框架使用的jar包（XposedBridge.jar）加载到android虚拟机中，然后将所有xposed插件模块也加载进android虚拟机中，同时还会修改android的art虚拟机（libart.so）, 最后xposed通过ArtHook修改指定java方法的ArtMethod入口为代理函数。
- 因为zygote之后fork其他进程的时候会共享这些资源，所以所有的apk都会加载所有的xposed模块（这也是卡顿和费电的原因）。另外因为这些操作是在zygote进程启动的时候执行的，所以如果要更改或添加新的xposed模块就需要重新启动手机，因为zygote fork其他apk进程的时候并不会重新执行加载xposed模块的代码了

