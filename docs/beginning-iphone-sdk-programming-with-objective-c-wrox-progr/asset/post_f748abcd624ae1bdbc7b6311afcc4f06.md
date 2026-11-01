
> NOTE Note that the preceding statement works only for iPhone and not iPod Touch, because the iPod Touch does not have phone capabilities. Also, you would need a real device to test this out, the code does not have an effect on the iPhone Simulator. Appendix E discusses how to prepare your iPhone for testing.

## INTERCEPTING SMS MESSAGES

One of the most requested features of the iPhone SDK is the ability to intercept incoming SMS messages from within an iPhone application. Unfortunately, the current version of the SDK does not provide a means to do this.

Likewise, you cannot send SMS messages directly from within your application; the messages must be sent from the built-in SMS application itself. This requirement prevents rogue applications from sending SMS messages without the user's knowledge.

## ACCESSING THE CAMERA AND THE PHOTO LIBRARY

The iPhone and iPod Touch both have cameras that allow you to take pictures as well as record videos. All the pictures taken and videos recorded are saved in the Photos application. As a developer, you have a number of options to manipulate the cameras as well as access the pictures and videos stored in the Photos application:

- You can invoke the Camera to take pictures or record a video.
- You can invoke the Photos application to allow users to select a picture or video from the photo albums. You can then use the picture or video selected in your application.

### Accessing the Photo Library

Every iPhone and iPod Touch device includes the Photos application, in which all the pictures taken and videos recorded are stored. Using the iPhone SDK, you can use the UIImagePickerController class to programmatically display a UI to let the user select your pictures and videos from the Photos application. The following Try It Out demonstrates how you can do that in your application.

## TRY IT OUT Accessing the Photo Library

*Codefile [PhotoLibrary.zip] is available for download at Wrox.com*

1. Using Xcode, create a View-based Application project and name it PhotoLibrary.
2. Double-click the PhotoLibraryViewController.xib file to edit it in Interface Builder.
3. Populate the View window with the following views (see Figure 16-5):
   - Button
   - ImageView
4. In the Attributes Inspector window for the ImageView view, set the Mode to Aspect Fit.
5. In the PhotoLibraryViewController.h file, insert the following statements that appear in bold:
6. Back in Interface Builder, Control-click and drag the File's Owner item to the ImageView view and select imageView.
7. Control-click and drag the Button view to the File's Owner item select btnClicked.
8. In the PhotoLibraryViewController.m file, insert the following statements that appear in bold:

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

FIGURE 16-5

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

UIImagePickerController class uses the navigation controller to allow users to select the photos in the photo library. Therefore, you first need to specify the protocols in PhotoLibraryViewController.h:

```
@interface PhotoLibraryViewController : UIViewController
<UINavigationControllerDelegate, UIImagePickerControllerDelegate> {
...
```

When the Load Library button is clicked, you set the type of picker interface displayed by the UIImagePickerController class and then display it modally:

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

Note that if you want the picture to be editable when the user chooses the picture, you can add the following statement:

```
imagePicker.allowsImageEditing = YES;
```

By default, the source type is always UIImagePickerControllerSourceTypePhotoLibrary. However, you can also change it to one of the following:

- UIImagePickerControllerSourceTypeCamera
- UIImagePickerControllerSourceTypeSavedPhotosAlbum

When a picture/video has been selected by the user, the imagePickerController:didFinishPickingMediaWithInfo: event fires, and you handle it by checking the type of media selected by the user:

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

## TRY IT OUT — Activating the Camera

1. Using the same project created in the previous section, edit the `PhotoLibraryViewController.m` file and change the source type of the Image Picker to camera (see code highlighted in bold):

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

2. In the `PhotoLibraryViewController.h` file, declare the following two methods highlighted in bold so that you can save the image captured by the camera to the application’s Documents folder (on the device):

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

3. In the `PhotoLibraryViewController.m` file, define the two methods that you have declared in the previous step:

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
