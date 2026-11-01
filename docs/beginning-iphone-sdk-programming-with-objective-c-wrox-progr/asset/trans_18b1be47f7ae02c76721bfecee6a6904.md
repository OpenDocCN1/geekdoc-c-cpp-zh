

> 注意：上述语句仅适用于 iPhone，而不适用于 iPod Touch，因为 iPod Touch 不具备电话功能。另外，你需要使用真机来测试这一点，该代码在 iPhone 模拟器上不会产生效果。附录 E 讨论了如何准备你的 iPhone 进行测试。

## 拦截短信

iPhone SDK 中最常被要求的功能之一是从 iPhone 应用程序内拦截传入的短信。遗憾的是，当前版本的 SDK 并没有提供实现这一功能的方法。

同样，你也不能直接从应用程序中发送短信；短信必须通过内置的短信应用本身发送。这个要求可以防止恶意应用程序在用户不知情的情况下发送短信。

## 访问摄像头和照片图库

iPhone 和 iPod Touch 都配有摄像头，可以用来拍照和录制视频。所有拍摄的照片和录制的视频都会保存在“照片”应用程序中。作为开发者，你有很多选项可以用来操作摄像头，以及访问存储在“照片”应用程序中的照片和视频：

-   你可以调用摄像头来拍照或录制视频。
-   你可以调用“照片”应用程序，让用户从相册中选择照片或视频，然后你可以在应用程序中使用所选的照片或视频。

### 访问照片图库

每部 iPhone 和 iPod Touch 设备都包含“照片”应用程序，其中存储了所有拍摄的照片和录制的视频。使用 iPhone SDK，你可以使用 `UIImagePickerController` 类以编程方式显示一个界面，让用户从“照片”应用程序中选择你的照片和视频。下面的“动手实验”演示了如何在应用程序中实现这一点。

## 动手实验：访问照片图库

*代码文件 [PhotoLibrary.zip] 可从 Wrox.com 下载*

1.  使用 Xcode 创建一个基于视图的应用程序项目，并将其命名为 `PhotoLibrary`。
2.  双击 `PhotoLibraryViewController.xib` 文件，在 Interface Builder 中编辑它。
3.  在 View 窗口中添加以下视图（参见图 16-5）：
    -   Button
    -   ImageView
4.  在 ImageView 视图的 Attributes Inspector 窗口中，将 Mode 设置为 Aspect Fit。
5.  在 `PhotoLibraryViewController.h` 文件中，插入以下以粗体显示的语句：
6.  回到 Interface Builder 中，按住 Control 键并将 File's Owner 项拖到 ImageView 视图上，然后选择 `imageView`。
7.  按住 Control 键并将 Button 视图拖到 File's Owner 项上，选择 `btnClicked`。
8.  在 `PhotoLibraryViewController.m` 文件中，插入以下以粗体显示的语句：

```
#import <UIKit/UIKit.h>

@interface PhotoLibraryViewController : UIViewController
<UINavigationControllerDelegate,
UIImagePickerControllerDelegate> {
    IBOutlet UIImageView *imageView;
    UIImagePickerController *imagePicker;
}

@property (nonatomic, retain) UIImageView *imageView;

- (IBAction)btnClicked:(id)sender;

@end
```

```
#import "PhotoLibraryViewController.h"

@implementation PhotoLibraryViewController

@synthesize imageView;

- (void)viewDidLoad {
    imagePicker = [[UIImagePickerController alloc] init];
```

![](img/16991b58db5894715c4a443315e06a22_390_0.png)

图 16-5

```
[super viewDidLoad];
}
- (IBAction) btnClicked: (id) sender{
    imagePicker.delegate = self;
    imagePicker.sourceType = UIImagePickerControllerSourceTypePhotoLibrary;

    //---show the Image Picker---
    [self presentModalViewController:imagePicker animated:YES];
}
- (void)imagePickerController:(UIImagePickerController *)picker
 didFinishPickingMediaWithInfo:(NSDictionary *)info {
    UIImage *image;
    NSURL *mediaUrl;

    mediaUrl = (NSURL *)[info valueForKey:UIImagePickerControllerMediaURL];

    if (mediaUrl == nil)
    {
        image = (UIImage *)[info valueForKey:UIImagePickerControllerEditedImage];
        if (image == nil)
        {
            //---original image selected---
            image = (UIImage *)
            [info valueForKey:UIImagePickerControllerOriginalImage];

            //---display the image---
            imageView.image = image;
        }
        else //---edited image picked---
        {
            //---get the cropping rectangle applied to the image---
            CGRect rect =
            [[info valueForKey:UIImagePickerControllerCropRect] CGRectValue ];

            //---display the image---
            imageView.image = image;
        }
    }
    else
    {
        //---video picked---
        //...
    }

    //---hide the Image Picker---
    [picker dismissModalViewControllerAnimated:YES];
}
- (void)imagePickerControllerDidCancel:(UIImagePickerController *)picker
```

`UIImagePickerController` 类使用导航控制器来让用户选择照片图库中的照片。因此，你首先需要在 `PhotoLibraryViewController.h` 中指定协议：

```
@interface PhotoLibraryViewController : UIViewController
<UINavigationControllerDelegate, UIImagePickerControllerDelegate> {
...
```

当点击“加载图库”按钮时，你设置 `UIImagePickerController` 类所显示的选取器界面类型，然后以模态方式显示它：

```
- (IBAction) btnClicked: (id) sender {
    //---the delegate that implements the methods defined in the protocols---
    imagePicker.delegate = self;
    //---type of source---
    imagePicker.sourceType = UIImagePickerControllerSourceTypePhotoLibrary;
    //---show the Image Picker---
    [self presentModalViewController:imagePicker animated:YES];
}
```

请注意，如果你希望用户选择图片时可以编辑图片，可以添加以下语句：

```
imagePicker.allowsImageEditing = YES;
```

默认情况下，源类型始终是 `UIImagePickerControllerSourceTypePhotoLibrary`。不过，你也可以将其更改为以下任一项：

-   `UIImagePickerControllerSourceTypeCamera`
-   `UIImagePickerControllerSourceTypeSavedPhotosAlbum`

当用户选好图片/视频后，`imagePickerController:didFinishPickingMediaWithInfo:` 事件会触发，你可以通过检查用户所选媒体的类型来处理该事件：

```
- (void)imagePickerController:(UIImagePickerController *)picker didFinishPickingMediaWithInfo:(NSDictionary *)info {
    UIImage *image;
    NSURL *mediaUrl;
    mediaUrl = (NSURL *)[info valueForKey:UIImagePickerControllerMediaURL];
    if (mediaUrl == nil) {
        image = (UIImage *)[info valueForKey:UIImagePickerControllerEditedImage];
        if (image == nil) {
            //---original image selected---
            image = (UIImage *)
```

## 动手实验——激活摄像头

1.  使用上一节中创建的同一个项目，编辑 `PhotoLibraryViewController.m` 文件，并将 Image Picker 的源类型更改为摄像头（参见以下以粗体显示的代码）：

```objective-c
-(IBAction) btnClicked: (id) sender{
    imagePicker.delegate = self;

    //---comment this out---
    //imagePicker.sourceType = UIImagePickerControllerSourceTypePhotoLibrary;

    //---invoke the camera---
    imagePicker.sourceType = UIImagePickerControllerSourceTypeCamera;

    imagePicker.allowsImageEditing = YES;
    [self presentModalViewController:imagePicker animated:YES];
}
```

2.  在 `PhotoLibraryViewController.h` 文件中，声明以下两个以粗体显示的方法，以便你可以将摄像头拍摄的图像保存到应用程序的 Documents 文件夹中（在设备上）：

```objective-c
#import <UIKit/UIKit.h>

@interface PhotoLibraryViewController : UIViewController
    < UINavigationControllerDelegate, UIImagePickerControllerDelegate> {

    IBOutlet UIImageView *imageView;
    UIImagePickerController *imagePicker;
}

@property (nonatomic, retain) UIImageView *imageView;

-(IBAction) btnClicked: (id) sender;

- (NSString *) filePath: (NSString *) fileName;
- (void) saveImage;

@end
```

3.  在 `PhotoLibraryViewController.m` 文件中，定义你在上一步中声明的两个方法：

```objective-c
- (NSString *) filePath: (NSString *) fileName {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(
                         NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDir = [paths objectAtIndex:0];
    return [documentsDir stringByAppendingPathComponent:fileName];
}

- (void) saveImage{
    //---get the data from the ImageView---
    NSData *imageData =
        [NSData dataWithData:UIImagePNGRepresentation(imageView.image)];
```

