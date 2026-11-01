# TRY IT OUT — **Activating the Camera**

+   1. Using the same project created in the previous section, edit the `PhotoLibraryViewController.m` file and change the source type of the Image Picker to camera (see code highlighted in bold):

```
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
```

+   2. In the `PhotoLibraryViewController.h` file, declare the following two methods highlighted in bold so that you can save the image captured by the camera to the application’s Documents folder (on the device):

```
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
```

+   3. In the `PhotoLibraryViewController.m` file, define the two methods that you have declared in the previous step:

```
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
```