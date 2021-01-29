# LiteKit接入文档

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

LiteKit是基于端推理框架LiteKitCore和端推理引擎PaddleLite，面向移动端工程师的AI能力解决方案。
LiteKit旨在为客户端应用提供开箱即用的离线的AI能力，使产品快速的简单的接入AI能力，并将提供的AI能力应用于各种业务场景。

目前已经支持的人像分割、手势识别、视频超分均来自百度各个产品线，已上线功能中，中台化输出的AI能力。

## 快速体验

### 效果展示
| 手势识别 | 人像分割 |
| --- | --- |
| <div align=center><img width="320" height="480"  src="/Doc/Resources/1_5.gif"/></div> | <div align=center><img width="320" height="315"  src="/Doc/Resources/1_6.gif"/></div> |

视频超分
| 超分前 | 超分后 |
| --- | --- |
| ![SR](/Doc/Resources/1_7.jpeg) | ![SR](/Doc/Resources/1_7_2.png) |
### 1. Android - 扫码安装<br>
![QR_Code](/Doc/Resources/1_3.png)

### 2. Demo Project

```
git clone https://github.com/PaddlePaddle/LiteKit.git
```


#### iOS平台
示例工程中展示了人像分割、手势识别、视频超分能力。包括能力的接入demo和能力效果的展示。

###### 示例工程部署
```
cd LiteKit/LiteKitDemo/iOS/LiteKitDemo
pod install --repo-update
open LiteKitDemo.xcworkspace
```
运行工程可在真机测试机上查看效果。


#### Android平台
1. 打开Android Studio，点击File->Open...，选择LiteKitDemo/Android目录
2. 参考[LiteKit README](/LiteKit/LiteKitDemo/Android/README.md)文档，下载并放置依赖aar至对应位置
3. 点击Run安装运行到真机上（Demo中视频检测依赖摄像头输入）


## 依赖关系

LiteKit依赖关系如下：
<p align="center"><img width="300" src="/Doc/Resources/1_4.png"/></p>

其中：
1. PaddleLite层，[PaddleLite](https://github.com/PaddlePaddle/Paddle-Lite)是一个高性能、轻量级、灵活性强且易于扩展的深度学习推理框架，LiteKitSDK的AI能力底层基于PaddleLite引擎实现。
2. LiteKitCore层，LiteKitCore是一种跨平台的，面向移动开发者的，AI工程化的综合解决方案。LiteKitCore作为端模型预测的统一接入层，目的是端模型的快速工程化集成，降低客户端RD在端运行AI模型的门槛和提升集成效率，同时也能更好实现基于端模型业务能力的快速横向输出。目前为提供了Objective C，Java，C++三种语言的API。
3. LiteKit层，视频超分，人像分割，手势识别，均称为LiteKit的业务SDK。每种业务SDK中，封装了对应AI能力的模型、预测的前后处理等逻辑。后续会产生更多覆盖其他AI场景的业务SDK。

### 1. 依赖
LiteKit由[MIT License](LICENSE)提供

|依赖 | iOS版本| Android版本 |
|---|---|---|
|LiteKitHandGestureDetection    | 0.1.0 | 0.1.0 | 
|LiteKitPortraitSegmentation      | 0.1.0 | 0.1.0 |
|LiteKitAIVideoSuperResolution  | 0.1.0 | 0.1.0 |

### 2. 安装SDK
[接入文档 for iOS](/Doc/LiteKit接入文档(for%20iOS).md) <br>
[接入文档 for Android](/Doc/LiteKit接入文档(for%20Android).md)



## API
LiteKit的AI能力，主要包含3类接口：创建、执行、释放。
使用时，先通过创建接口创建对应的预测引擎实例，之后可以通过执行接口进行预测，当使用完毕后需要对预测引擎实例进行释放。
其中执行接口通常有多个，可以接受不同格式的数据输入，以适应相机帧、图像、视频解码数据等不同也业务场景。

<p align="center"><img width="300" src="/Doc/Resources/1_8.png"/></p>

[人像分割](/Doc/LiteKit接口文档_人像分割.md) <br>
[手势识别](/Doc/LiteKit接口文档_手势识别.md) <br>
[视频超分](/Doc/LiteKit接口文档_视频超分.md) <br>


## 隐私说明
LiteKit目前版本不会收集任何用户数据和用户信息，也不需要申请用户的隐私权限。

## 交流与反馈
<p align="center"><img width="200" height="200"  src="https://user-images.githubusercontent.com/45189361/64117959-1969de80-cdc9-11e9-84f7-e1c2849a004c.jpeg"/></p>
<p align="center">&#8194;&#8194;&#8194;微信公众号&#8194;&#8194;&#8194;&#8194;</p>


## 版权和许可证
LiteKit由[MIT License](LICENSE)提供

# LiteKitCore接入文档
## 一、介绍
### 1. 背景
LiteKitCore是一种跨平台的，面向移动开发者的，AI工程化的综合解决方案。LiteKitCore作为端模型预测的统一接入层，目的是端模型的快速工程化集成，降低客户端RD在端运行AI模型的门槛和提升集成效率，同时也能更好实现基于端模型业务能力的快速横向输出。基于LiteKitCore的端AI预测能力，可以快速的基于不同宿主进行集成与部署。LiteKitCore主要功能如下：模型加载，预测能力，前后处理能力，业务数据到Backend Input/Output的转换，Backend无感知升级，性能统计，容错处理，任务队列管理，运行时资源调度，生命周期管理等。


### 2. 兼容性
支持平台：iOS、Android、Native C++ 。<br>
支持Backend：支持PaddleMobile/Paddle-Lite/BML(LR/GBDT)等Backend。 


### 3. 依赖和体积
#### iOS平台
###### Native C++ API

| 依赖 | 版本 | 体积 | 
|---|---|---|
| LiteKit Native | 0.0.9 | 51.5MB(armv7), 51MB(arm64) |

###### Objective-C API
|依赖| 版本|体积 | 
|---|---|---|
|LiteKit|0.0.9|3.3MB|
|opencv|3.4.1|128.6MB|
|paddleLite|1.0.0|102.2MB|
|paddle_mobile|1.0.0|14.1MB|
|ProtocolBuffers|1.0.0|18.7MB|
|ZipArchive|1.0.0|3.9MB|


#### Java API 依赖
|依赖|版本| 体积 | 
|---|---|---|
| LiteKit Native|-|51.5MB(armv7), 51MB(arm64) |

### 4. Demo Project
iOS示例工程包含了Native C++ API和Objective-C API的demo调用示例，Native C++ API和Objective-C API分别包含CPU和GPU两种backend，一共4种加载和预测的方式。针对C++API（在iOS上）和Objective-C API的CPU/GPU backend分别是对齐的，模型的加载和预测能力一致。但是CPU和GPU backend之间是隔离的，预测所使用的模型是不一样的。

#### 示例iOS工程部署
1.组装工程 
```
git clone https://github.com/PaddlePaddle/LiteKit.git
cd PaddleLiteKitCore/LiteKitDemo/iOS
open LiteKitDemo.xcodeproj
```
2.配置调试真机及Apple ID
![图片](/Doc/Resources/1_1.png)

3.运行示例工程
![图片](/Doc/Resources/1_2.png)
|类名 | 说明 | 
|---|---|
|ViewController |LiteKit（Objective-C & C++）以GPU、CPU作为backend的load及predict的demo code |
| ViewController+LiteKitCore_CPP | LiteKit Native C++ API load demo code|
| ViewController+LiteKitCore_OC | LiteKit Objective-C API load demo code|

#### 部署Android示例工程  
1. 首先编译[LiteKitCore/LiteKit/C++](LiteKitCore/LiteKit/C%2B%2B/README.md), 生成`libLiteKit_framework.so`
2. 然后编译[LiteKitCore/LiteKit/Android](LiteKitCore/LiteKit/Android/README.md), 生成`LiteKitCore-debug.aar`
3. 最后编译[LiteKitCore/LiteKitDemo/Android](LiteKitCore/LiteKitDemo/Android/README.md), 通过Android studio 打开项目即可运行demo

## 二、接口文档
[接口文档 for Native C++ API](/Doc/LiteKitCore接口文档(for%20Native%20C%2B%2B%20API).md)
<br>
[接口文档 for Objective-C API ](/Doc/LiteKitCore接口文档(for%20Objective-C%20API).md)
<br>
[接口文档 for Java API ](/Doc/LiteKitCore接口文档(for%20Java%20API).md)

## 三、接入文档
[接入文档 for Objective-C API ](/Doc/LiteKitCore接入文档(for%20Objective-C%20API).md)
<br>
[接入文档 for Native C++ API on iOS](/Doc/LiteKitCore接入文档(for%20Native%20C%2B%2B%20API%20on%20iOS).md)
<br>
[接入文档 for Native C++ API on Android](/Doc/LiteKitCore接入文档(for%20Native%20C%2B%2B%20API%20on%20Android).md)
<br>
[接入文档 for Java API ](/Doc/LiteKitCore接入文档(for%20Java%20API).md)




