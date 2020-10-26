# MMLCore接入文档
## 一、介绍
## 1. 背景
MMLCore是一种业界领先的，跨平台的，面向移动开发者的，AI工程化的综合解决方案。MMLCore作为端模型预测的统一接入层，目的是端模型的快速工程化集成，降低客户端RD在端运行AI模型的门槛和提升集成效率，同时也能更好实现基于端模型业务能力的快速横向输出。基于MMLCore的端AI预测能力，可以快速的基于不同宿主进行集成与部署。MMLCore主要功能如下：模型加载，预测能力，前后处理能力，业务数据到Backend Input/Output的转换，Backend无感知升级，性能统计，容错处理，任务队列管理，运行时资源调度，生命周期管理等。


### 2. 兼容性
支持平台：iOS、Android、Native C++ 。
支持Backend：支持PaddleMobile/Paddle-Lite/BML(LR/GBDT)等Backend可供选择，同时支持Backend平行切换。 


### 3. 依赖和体积
#### iOS平台
###### Native C++ API

| 依赖 | 版本 | 体积 | 
|-------|------|-------|
| MML Native | - | 51.5MB(armv7), 51MB(arm64) |

###### OC API
|依赖| 版本|体积 | 
|----|----|----|----|
|MML|1.0.0|3.3MB|
|opencv|3.4.1|128.6MB|
|paddleLite|1.0.0|102.2MB|
|paddle_mobile|1.0.0|14.1MB|
|ProtocolBuffers|1.0.0|18.7MB|
|ZipArchive|1.0.0|3.9MB|


#### Android API 依赖
|依赖|版本| 体积 | 
|---|---|---|---|
| MML Native|-|51.5MB(armv7), 51MB(arm64) |

### 4. Demo Project
#### 示例工程说明
iOS示例工程包含了Native C++ API和OC API的demo调用示例，Native C++ API和OC API分别包含CPU和GPU两种backend，一共4种加载和预测的方式。针对C++和OC的CPU/GPU backend分别是对齐的，模型的加载和预测能力一致。但是CPU和GPU之间是隔离的，预测所使用的模型是不一样的。

#### 示例IOS工程部署
1.组装工程 
```
git clone https://github.com/PaddlePaddle/LiteKit.git
cd PaddleMMLCore/MMLDemo/iOS
pods install
open MMLDemo.xcodeproj
```
2.配置调试真机及Apple ID
![图片](https://agroup-bos-bj.cdn.bcebos.com/bj-afca654008a9396cf3c9f219867eae4f219418af)

3.运行示例工程
![图片](https://agroup-bos-bj.cdn.bcebos.com/bj-38ae6dc1d29f975995e990ed09e93b0bb7d0f115)
说明：
|类名 | 说明 | 
|---|---|---|---|
|ViewController |MML（OC & C++）以GPU、CPU作为backend的load及predict的demo code |
| ViewController+MMLCore_CPP | MML Native C++ API load demo code|
| ViewController+MMLCore_OC | MML OC API load demo code|

#### 部署Android示例工程  
1. 首先编译[MMLCore/MML/C++](MML/C++/README.md), 生成`libmml_framework.so`
2. 然后编译[MMLCore/MML/Android](MML/Android/README.md), 生成`mmlcore-debug.aar`
3. 最后编译[MMLCore/MMLDemo/Android](MMLDemo/Android/README.md), 通过Android studio 打开项目即可运行demo

## 二、接口文档
[接口文档 for Native C++ API on iOS](http://agroup.baidu.com/wangzhiyong04/md/article/3455104)
[接口文档 for OC API ](http://agroup.baidu.com/wangzhiyong04/md/article/3461715)
[TODO——接口文档 for Android API ]()

## 三、接入文档
[接入文档 for OC API ](http://agroup.baidu.com/wangzhiyong04/md/article/3460708)
[接入文档 for Native C++ API on iOS](http://agroup.baidu.com/wangzhiyong04/md/article/3460370)
[TODO —— 接入文档 for Native C++ API on Android]()
[TODO —— 接入文档 for Android API ]()




