
//---write the data to file---
[imageData writeToFile:[self filePath:@"MyPicture.png"] atomically:YES];
}

- 4. 在 Xcode 中右键单击 Frameworks 组并选择添加 ⇧ 现有框架。选择 Frameworks/MediaPlayer.framework。

- 5. 在 PhotoLibraryViewController.h 文件中，导入以下头文件：

```
#import <UIKit/UIKit.h>
#import <MediaPlayer/MediaPlayer.h>
```

- 6. 插入以下以粗体显示的语句：

```
- (void)imagePickerController:(UIImagePickerController *)picker didFinishPickingMediaWithInfo:(NSDictionary *)info {
    UIImage *image;
    NSURL *mediaUrl;
    
    mediaUrl = (NSURL *)[info valueForKey:UIImagePickerControllerMediaURL];
    if (mediaUrl == nil) {
        image = (UIImage *)[info valueForKey:UIImagePickerControllerEditedImage];
        if (image == nil) {
            //---original image selected---
            image = (UIImage *)[info valueForKey:UIImagePickerControllerOriginalImage];
            //---display the image---
            imageView.image = image;
            //---save the image captured---
            [self saveImage];
        } else {
            //---edited image picked---
            //---get the cropping rectangle applied to the image---
            CGRect rect = [[info valueForKey:UIImagePickerControllerCropRect] CGRectValue];
            //---display the image---
            imageView.image = image;
            //---save the image captured---
            [self saveImage];
        }
    } else
{ //---video picked---
MPMoviePlayerController *player = [[MPMoviePlayerController alloc]
    initWithContentURL:mediaUrl];
[player play];
}
//---hide the Image Picker---
[picker dismissModalViewControllerAnimated:YES];
}
```

- 7. 按 Command-R 在真实的 iPhone 上测试应用程序。

> NOTE 附录 E 讨论了如何为测试准备您的 iPhone。

- 8. 点击 Load Photo Library 按钮，现在您可以使用 iPhone 的相机拍摄照片和视频。如果您用它拍照，您拍摄的照片会保存到应用程序的 Document 文件夹中。如果您拍摄视频，视频可以使用设备上的媒体播放器回放。

## 工作原理

在本练习中，您所做的是将 Image Picker 的源类型修改为相机：

```
imagePicker.sourceType = UIImagePickerControllerSourceTypeCamera;
```

当相机拍摄照片时，照片会通过 imagePickerController:didFinishPickingMediaWithInfo: 方法传回并显示在 ImageView 视图中。但是，手动将图像保存到手机上的位置是您的责任。在这种情况下，您定义了 filePath: 方法以将照片保存到应用程序的 Document 文件夹中：

```
- (NSString *) filePath: (NSString *) fileName {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(
        NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDir = [paths objectAtIndex:0];
    return [documentsDir stringByAppendingPathComponent:fileName];
}
```

saveImage: 方法提取 ImageView 视图上的图像数据，然后调用 filePath: 方法将数据保存到名为 MyPicture.png 的文件中：

```
- (void) saveImage{
    //---get the data from the ImageView---
    NSData *imageData =
    [NSData dataWithData:UIImagePNGRepresentation(imageView.image)];
    //---write the data to file---
    [imageData writeToFile:[self filePath:@"MyPicture.png"] atomically:YES];
}
```

## 工作原理

与前面使用 UIImagePickerController 类从照片库中选择照片的部分类似，您也可以使用 ABPeoplePickerNavigationController 类访问 iPhone 上通讯录应用程序中存储的联系人。在使用 ABPeoplePickerNavigationController 类之前，您需要将 AddressBook 和 AddressBookUI 框架添加到项目中。与 UIImagePickerController 类类似，您需要遵循特定的协议，具体来说是 ABPeoplePickerNavigationControllerDelegate 协议。本质上，在您从通讯录应用程序中选择联系人后，可能会调用以下方法：

- peoplePickerNavigationController:shouldContinueAfterSelectingPerson:
- peoplePickerNavigationController:shouldContinueAfterSelectingPerson:property:identifier:
- peoplePickerNavigationControllerDidCancel:

peoplePickerNavigationControllerDidCancel: 方法会在您在从通讯录应用程序中选择联系人时点击取消按钮时触发。

当您点击联系人时，peoplePickerNavigationController:shouldContinueAfterSelectingPerson: 方法会被触发。所选联系人的详细信息被封装在 shouldContinueAfterSelectingPerson: 参数中，其类型为 ABRecordRef。

在此示例中，您提取了联系人的各种属性并使用 AlertView 类将其显示出来：

```
//---get the First Name---
NSString *str = (NSString *)ABRecordCopyValue(person,
    kABPersonFirstNameProperty);
str = [str stringByAppendingString:@"\n"];

//---get the Last Name---
str = (NSString *)ABRecordCopyValue(
    person, kABPersonLastNameProperty);
str = [str stringByAppendingString:@"\n"];

//---get the Emails---
ABMultiValueRef emailInfo = ABRecordCopyValue(person, kABPersonEmailProperty);

//---iterate through the emails---
for (NSUInteger i=0; i < ABMultiValueGetCount(emailInfo); i++) {
    str = [str stringByAppendingString:
        (NSString *)ABMultiValueCopyValueAtIndex(emailInfo, i)];
    str = [str stringByAppendingString:@"\n"];
}

//---display the details---
UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Selected Contact"
                                 message:str delegate:self
                                 cancelButtonTitle:@"OK"
                                 otherButtonTitles:nil];
[alert show];
[alert release];
```

```objective-c
{
    ABRecordRef ref = CFArrayGetValueAtIndex(allContacts, i);
    NSString *contactFirstName = (NSString *) ABRecordCopyValue(
        ref, kABPersonFirstNameProperty);
    NSString *contactLastName = (NSString *) ABRecordCopyValue(
        ref, kABPersonLastNameProperty);

    if ( [firstName isEqualToString:contactFirstName] &&
         [lastName isEqualToString:contactLastName] )
    {
        ABAddressBookRemoveRecord(addressBook, ref, nil);
        ABAddressBookSave(addressBook, nil);
    }
}
```

前述方法 `removeContact` 接受两个参数 `firstName` 和 `lastName`，并在通讯录应用程序中搜索具有匹配名字和姓氏的联系人。如果找到联系人，则将其从通讯录应用程序中删除。

> **NOTE** 有关删除联系人所使用的各种方法的更多信息，请参阅 Apple iPhone 参考资料库中的 ABAddressBook 参考。您可以在 `http://developer.apple.com/iphone/library/documentation/AddressBook/Reference/ABAddressBookRef_iPhoneOS/ABAddressBookRef_iPhoneOS.pdf` 下载该参考资料。

## 摘要

在本章中，您了解了如何轻松地将各种内置应用程序集成到自己的 iPhone 应用程序中。特别是，您了解了如何仅通过使用 URL 字符串来调用内置的 SMS、Mail、Safari 和电话拨号器。您还学习了如何使用 iPhone SDK 提供的类访问通讯录和照片库。

## 练习：

- 1. 命名用于调用 Safari、Mail、SMS 和电话拨号器应用程序的各种 URL 字符串。
- 2. 在 iPhone 中调用 Image Picker UI 的类名是什么？
- 3. 在 iPhone 中调用 People Picker UI 的类名是什么？

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| 在应用程序内部发送电子邮件 | NSString *emailString = @"mailto:?to=USER@EMAIL.COM&subject=SUBJECT&body=BODY OF EMAIL"; [[UIApplication sharedApplication] openURL:[NSURL URLWithString:emailString]]; |
| 调用 Safari | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"http://www.apple.com"]]; |
| 调用电话 | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"tel:1234567890"]]; |
| 调用短信 | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"sms:96924065"]]; |
| 访问照片库 | 使用 UIImagePickerController 类并确保您的视图控制器符合 UINavigationControllerDelegate 协议。 |
| 访问通讯录应用程序 | 使用来自 AddressBookUI 框架的 ABPeoplePickerNavigationController 类。 |

