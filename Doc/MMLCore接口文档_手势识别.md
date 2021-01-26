# 手势识别接口文档
手势识别能力由LiteKit HandGestureDetection SDK提供的，实时的手势检测能力。可以准确的检测手势所在的位置、手势类型、置信度。

## 检测内容
- 手势类型
- 手势位置
- 置信度



//TODO 
## iOS

### 数据模型
1. MMLHandGestureDetectionLabel：可识别手势类型的枚举的定义，目前支持6种。

| 手势| 说明 | 图例 |
| --- | --- | --- |
| 手  | MMLHandGestureDetectionLabelHand = 0 |  |
| 五指 | MMLHandGestureDetectionLabelFive = 1 |  |
| V手势 | MMLHandGestureDetectionLabelVictory = 2 |  |
| 比心 | MMLHandGestureDetectionLabelFist = 3 |  |
| 一指 | MMLHandGestureDetectionLabelOne = 4 |  |
| OK手势| MMLHandGestureDetectionLabelOK = 5 |  |

2. MMLHandGestureDetectResult：手势识别结果数据结构的定义
```objective-c
/**
 * define hand gesture detect result data
 */
@interface MMLHandGestureDetectResult : NSObject
```

手所在位置，基于图像左上角顶点的rect。
```objective-c
// rect of hand‘s bounding box
@property (nonatomic, assign, readonly) CGRect handBoxRect;
```

手指尖所在位置，基于图像左上角顶点的point。
```objective-c
// position of finger
@property (nonatomic, assign, readonly) CGPoint fingerPoint;
```

手势类型的枚举，详见MMLHandGestureDetectionLabel的说明。
```objective-c
// label of detection result
@property (nonatomic, assign, readonly) MMLHandGestureDetectionLabel label;
```

置信度会返回0～1之间的值
```objective-c
// confidence of detection result
@property (nonatomic, assign, readonly) float confidence;

@end
```
手势识别detector的API，通过createGestureDetector创建detector之后，可以通过UIImage、CMSampleBufferRef、uint8_t * 三种数据作为input执行预测。
```objective-c
/**
 * hand gesture detector
 */
@interface MMLHandGestureDetector : NSObject

/**
 * @brief initialize and return a instance of gesture detector, the model should be put in main bundle
 *
 * @param error if an error occurs, this param will carry the information
 * @return a instance of gesture detector
 */
+ (instancetype)createGestureDetector:(NSError **)error;

/**
 * @brief initialize and return a instance of gesture detector with model path
 *
 * @param path the folder where the model is located
 * @param error if an error occurs, this param will carry the information
 * @return a instance of gesture detector
 */
+ (instancetype)createGestureDetectorWithModelPath:(NSString *)path error:(NSError **)error;

/**
 * @brief detect hand gesture with image
 *
 * @param image UIImage that will be detected
 * @param complete completion block with result and error imformation
 */
- (void)detectWithUIImage:(UIImage *)image
                 complete:(void (^)(MMLHandGestureDetectResult *result, NSError *error))complete;

/**
 * @brief detect hand gesture with sampleBuffer
 *
 * @param sampleBuffer sampleBuffer that will be detected
 * @param complete completion block with result and error imformation
 */
- (void)detectWithSampleBuffer:(CMSampleBufferRef)sampleBuffer
                      complete:(void (^)(MMLHandGestureDetectResult *result, NSError *error))complete;

/**
 * @brief detect hand gesture with pixelRawData
 *
 * @param pixelRawData pixelRawData that will be detected, pixel format shoud be RGBA
 * @param width detect buffer width
 * @param height detect buffer height
 * @param complete completion block with result and error imformation
 */
- (void)detectWithPixelRawData:(uint8_t *)pixelRawData
                         width:(int)width
                        height:(int)height
                      complete:(void (^)(MMLHandGestureDetectResult *result, NSError *error))complete;

@end
```


## Android
对手势识别的HandGestureDetector进行初始化
```java
example：HandGestureDetector.init(this, modelPath)

其中：
/**
 * @desc 对HandGestureDetector进行初始化
 * @param context 上下文context
 * @param modelFilePath 模型文件的地址（含模型名字）
 */
public static boolean init(Context context, String modelFilePath)
```

手势识别的预测接口
```java
example：HandGestureDetector.detect(scaleImage);

其中：
/**
 * @desc 通过bitmap进行预测
 * @param image 待预测的内容的bitmap
 * @return HandGestureDetectResult 预测结果
 */
public static HandGestureDetectResult detect(Bitmap image);

/**
 * @desc 通过byte数据进行预测
 * @param data 待预测的数据
 * @param imgWidth 图像Width
 * @param imgHeight 图像Height
 * @return HandGestureDetectResult 预测结果
 */
public static HandGestureDetectResult detect(byte[] data, int imgWidth, int imgHeight) 
```

预测返回结果结构HandGestureDetectResult
```java
public class HandGestureDetectResult {
    public RectF handBoxRect; // 识别出的手势的位置的的rect
    public PointF fingerPoint; // 手势中手指的位置的point
    public HandGestureDetectResult.GestureLabel label; // 识别出手势的类型
    public float confidence; // 置信度

    public static enum GestureLabel {
        Hand, //手
        Five, // 五指手势
        Victory, // 胜利V手势
        Fist, // 握拳手势
        One, // 指/1手势
        OK; // OK手势

        private GestureLabel() {
        }
    }
}
```

使用完成之后，对手势识别进行释放
```java
example:HandGestureDetector.release();

其中
/**
 * @desc 对HandGestureDetector中需要释放的资源进行释放
 */
public static boolean release()
```
