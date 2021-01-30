# LiteKit接入文档(for iOS)
## 导入SDK
通过pod引入，[参考](/LiteKit/LiteKitDemo/iOS/LiteKitDemo/Podfile)
```ruby
# coding: utf-8
source 'https://github.com/CocoaPods/Specs.git'

platform :ios

target 'LiteKitDemo' do
  project './LiteKitDemo.xcodeproj'
    platform :ios, '10.0'

    pod 'LiteKitHandGestureDetection', '~> 0.1.0'
    pod 'LiteKitPortraitSegmentation', '~> 0.1.0'
    pod 'LiteKitVideoSuperResolution', '~> 0.1.0'
end

```

## 使用方法
### 1. 人像分割
引入头文件
```objective-c
#import <LiteKitPortraitSegmentation/LiteKitPortraitSegmentor.h>
```

创建Predictor
```objective-c
LiteKitPortraitSegmentor *portraitSegmentor = [LiteKitPortraitSegmentor createPortraitSegmentorWithError:&error];
```

执行Predict、获取Output
```objective-c
LiteKitPSData *output = (LiteKitPSData *)[self.portraitSegmentor inferWithPixelBuffer:CMSampleBufferGetImageBuffer(sampleBuffer) error:nil];
```

释放Predictor
```objective-c
Predictor不需要特殊的释放操作
```

### 2. 手势识别
引入头文件
```objective-c
#import <LiteKitHandGestureDetection/LiteKitHandGestureDetector.h>
```

创建Predictor
```objective-c
LiteKitHandGestureDetector *gestureRecognizer = [LiteKitHandGestureDetector createHandGestureDetectorWithError:&error];
```

执行Predict、获取Output
```objective-c
//执行predict
[self.gestureRecognizer detectWithUIImage:self.image complete:^(LiteKitHandGestureDetectResult *result, NSError *error) {
    //result为获取的output
}];
```

释放Predictor
```objective-c
Predictor不需要特殊的释放操作
```

### 3. 视频超分
引入头文件
```objective-c
#import <LiteKitAIVideoSuperResolution/LiteKitAIVideoSuperResolution.h>
```

创建Predictor
```objective-c
LiteKitVideoSuperResolutionor *sVideo = [LiteKitVideoSuperResolutionor createVideoSuperResolutionorWithError:&error];
```

执行Predict、获取Output
```objective-c
// 执行predict，获取的newImg为output
UIImage *newImg = [sVideo superResolutionWithUIImage:self.image scale:1.0 error:&error];
```

释放Predictor
```objective-c
Predictor不需要特殊的释放操作
```
