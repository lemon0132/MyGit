# 人像分割接口文档

## iOS
人像分割能力的output数据结构定义
```objective-c
/**
 * @desc PortraitSegmentor data for output
 */
typedef struct MMLPortraitSegmentorData {
    struct MMLPortraitSegmentorDataShape {
        int n; // batch, =1
        int c; // channel, =1
        int h; // output height, =192
        int w; // output width, =192
    } dataShape; // output data shape
    uint8_t *data; // output data
} MMLPSData;

```
人像分割Segmentor的创建和执行，通过create方法创建Segmentor之后，可以以uint8_t、UIImage和CVPixelBufferRef三种作为input数据执行预测。
```objective-c
/**
 * @desc MML Portrait Segmentor Implement
 */
@interface MMLPortraitSegmentor : NSObject

#pragma mark - MMLPortraitSegmentor/Create

/**
 * @desc create Portrait Segmentor
 * @param modelPath Path for Portrait Segmentor model
 * @param error error while create, if succeed will be nil, nullable
 * @return instancetype Portrait Segmentor created
 */
+ (instancetype) create:(NSString *)modelPath
                  error:(NSError **)error;


#pragma mark - MMLPortraitSegmentor/Infer-Sync

/**
 * @desc Portrait Segmentor inference with RawData
 * @param rawData rawData to inference
 * @param width input Data width
 * @param height input data height
 * @param error  Error while inference, will be nil if succed
 * @return MMLPSData output data, size of 192*192
 */
- (MMLPSData *) inferWithRawData:(uint8_t *)rawData
                           width:(int)width
                          height:(int)height
                           error:(NSError **)error;

/**
 * @desc Portrait Segmentor inference with UIImage
 * @param image UIImage to inference
 * @param error  Error while inference, will be nil if succed
 * @return MMLPSData output data, size of 192*192
 */
- (MMLPSData *) inferWithImage:(UIImage *)image
                         error:(NSError **)error;

/**
 * @desc Portrait Segmentor inference with CVPixelBufferRef
 * @param pixelBuffer CVPixelBufferRef to inference
 * @param error  Error while inference, will be nil if succed
 * @return MMLPSData output data, size of 192*192
 */
- (MMLPSData *) inferWithPixelBuffer:(CVPixelBufferRef)pixelBuffer
                               error:(NSError **)error;

@end
```

## Android
人像分割的config定义MMLPortraitSegmentationConfig
```java
/**
 * @desc 设置config中的模型路径
 * @param path 模型路径
 */
public void setModelUrl(String path) 
```

初始化人像分割的MMLPortraitSegmentation
```java
/**
 * @desc 对MMLPortraitSegmentation进行初始化
 * @param config 初始化配置config
 */
public MMLPortraitSegmentation(MMLPortraitSegmentationConfig config)
```

人像分割MMLPortraitSegmentation的预测接口
```java
/**
 * @desc 通过byte数据进行预测
 * @param img_data 待预测的数据
 * @param imgWidth 图像Width
 * @param imgHeight 图像Height
 * @return int[] 预测结果
 */
public int[] predictor(byte[] img_data, int width, int height)

/**
 * @desc 通过bitmap数据进行预测
 * @param img_data 待预测的bitmap数据
 * @return int[] 预测结果
 */
public int[] predictor(Bitmap img_data)
```

释放人像分割资源

```java
/**
 * @desc 对人像分割MMLPortraitSegmentation进行释放
 */
public void release()
```
