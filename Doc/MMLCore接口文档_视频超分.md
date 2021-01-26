# 手势识别接口文档



## iOS
### 数据模型
视频超分使用的是YUV数据，以下为YUV数据结构定义，用于预测的input和output

```objective-c
///video frame YUV420 data struct
typedef struct {
    // frame width
    int width;
    // frame height
    int height;
    // data light (include Padding)
    int y_stride;
    int u_stride;
    int v_stride;
    //YUVdata
    uint8_t* y_data;
    uint8_t* u_data;
    uint8_t* v_data;
} MMLYUV420Data;//video 420 frame data

/**
 *release MMLYUVData
 * @param data input数据
 */
void releaseYUV420Data(MMLYUV420Data *data);

/**
 * copy MMLYUVData
 * @param src input data
 * @param dst output data
 */
void copyYUV420Data(const MMLYUV420Data *src, MMLYUV420Data *dst);

```
视频超分的config定义，需要在创建超分inferencer的时候，传入config。
config需要配置模型在工程中的位置。

```objective-c
/// video super resolution config
@interface MMLVideoSuperResolutionConfig : NSObject
/// model file dir
@property (nonatomic, strong) NSString *modelDir;

@end

```

视频超分能力inferencer，通过createInstanceWithConfig创建完成inferencer之后，可以通过
UIImage和MMLYUV420Data两种数据作为input执行超分。

```objective-c
/**
* creat Video superresolution inferencer
*/
@interface MMLVideoSuperResolutionor : NSObject

/**
 * @brief initialize and return a instance of video super resolutionor
 *
 * @param config config for superresolution
 * @param error if an error occurs, this param will carry the information
 * @return a instance of gesture detector
 */
+ (instancetype)createInstanceWithConfig:(MMLVideoSuperResolutionConfig *)config
                                   error:(NSError **)error;


/**
 * @brief execute videoSuperSolution
 *
 * @param inputData input data, struct MMLYUVData
 * @param outputData output data
 * @param error errorcode and error reason
 * @return BOOL YES for succeed，NO for failure
 */
- (BOOL)superResolutionWithInputData:(const MMLYUV420Data *)inputData
                          outputData:(MMLYUV420Data *)outputData
                               error:(NSError **)error;


/**
 * @brief execute videoSuperSolution
 *
 * @param inputImage input image, UIImage
 * @param error errorcode and error reason
 * @return UIImage image after superresolution
 */
- (UIImage *)superResolutionWithUIImage:(UIImage *)inputImage
                                  scale:(CGFloat)scale
                                  error:(NSError **)error;

@end
```




## Android
视频超分使用的是YUV数据，以下为YUV数据结构定义，用于预测的input和output

对视频超分SrBridge进行初始化方法
```java
example：SrBridge.nativeInitSr(FileManager.sr32(this));

其中：
/**
 * @desc 对SrBridge进行初始化
 * @param modelFilePath 模型文件的地址（含模型名字）
 * @return SrBridge的 handler，执行超分的时候需要使用
 */
public static native long nativeInitSr(String modelFilePath);
```

执行视频超分接口

```java

/**
 * @desc 对bitmap执行超分
 * @param handle SrBridge的handler
 * @param in input数据bitmap
 * @param scale scale倍数
 * @return Bitmap output数据bitmap
 */
public static native Bitmap nativePredictBitmap(long handle, Bitmap in, float scale);


/**
 * @desc 对bitmap执行超分
 * @param handle SrBridge的handler
 * @param in rgbabytearray数据rgba的数据数组
 * @param height input的height
 * @param width input的width
 * @param scale scale倍数
 * @return byte[] output数据
 */
public static native byte[] nativePredictRGBA(long handle, byte[] rgbabytearray, int height, int width, float scale);
    
```


释放超分SrBridge中JNI资源
```java
/**
 * @desc 对SrBridge进行释放
 */
public static native void nativeReleaseSrSdk(long handle);
```
