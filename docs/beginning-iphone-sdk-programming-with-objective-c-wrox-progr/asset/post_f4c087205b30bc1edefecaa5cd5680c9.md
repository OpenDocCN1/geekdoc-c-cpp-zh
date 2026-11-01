
//---write the data to file---
[imageData writeToFile:[self filePath:@"MyPicture.png"] atomically:YES];
}

- 4. Right-click the Frameworks group in Xcode and choose Add ⇧ Existing Frameworks. Select Frameworks/MediaPlayer.framework.

- 5. In the PhotoLibraryViewController.h file, import the following header file:

```
#import <UIKit/UIKit.h>
#import <MediaPlayer/MediaPlayer.h>
```

- 6. Insert the following statements that appear in bold:

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

- 7. Press Command-R to test the application on a real iPhone.

> NOTE Appendix E discusses how to prepare your iPhone for testing.

- 8. Tap the Load Photo Library button, and you are now able to use your iPhone's camera to take photos and videos. If you use it to take a picture, the picture you take is saved onto the Document folder of your application. If you take a video, the video can be played back using the media player on your device.

## How It Works

What you did in this exercise was modify the source type of the Image Picker to camera:

```
imagePicker.sourceType = UIImagePickerControllerSourceTypeCamera;
```

When the camera takes a picture, the picture is passed back in the imagePickerController:didFinishPickingMediaWithInfo: method and displayed in the ImageView view. However, it is your responsibility to manually save the image to a location on the phone. In this case, you defined the filePath: method to save the picture to the Document folder of your application:

```
- (NSString *) filePath: (NSString *) fileName {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(
        NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDir = [paths objectAtIndex:0];
    return [documentsDir stringByAppendingPathComponent:fileName];
}
```

The saveImage: method extracts the image data on the ImageView view and then calls the filePath: method to save the data into a file named MyPicture.png:

```
- (void) saveImage{
    //---get the data from the ImageView---
    NSData *imageData =
    [NSData dataWithData:UIImagePNGRepresentation(imageView.image)];
    //---write the data to file---
    [imageData writeToFile:[self filePath:@"MyPicture.png"] atomically:YES];
}
```

## How It Works

Like the previous section where you use the UIImagePickerController class to choose a photo from the Photo Library, you can also access the contacts stored in the Contacts application on your iPhone using the ABPeoplePickerNavigationController class. Before you use the ABPeoplePickerNavigationController class, you need to add the AddressBook and AddressBookUI frameworks to your project. Like the UIImagePickerController class, you need to conform to a specific protocol, specifically, the ABPeoplePickerNavigationControllerDelegate protocol. In essence, after you have selected a contact from the Contacts application, the following methods may be invoked:

- peoplePickerNavigationController:shouldContinueAfterSelectingPerson:
- peoplePickerNavigationController:shouldContinueAfterSelectingPerson:property:identifier:
- peoplePickerNavigationControllerDidCancel:

The peoplePickerNavigationControllerDidCancel: method is fired when you tap on the Cancel button when selecting a contact from the Contacts application.

When you tap on a contact, the peoplePickerNavigationController:shouldContinueAfterSelectingPerson: method is fired. The details of the selected contact are encapsulated in the shouldContinueAfterSelectingPerson: parameter, of type ABRecordRef.

In this example, you extracted the various properties of the contact and display it using the AlertView class:

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

The preceding method, `removeContact`, takes in two parameters, `firstName` and `lastName`, and searches the Contacts application for a contact with a matching first and last name. If a contact is found, it is removed from the Contacts application.

> **NOTE** For more information about the various methods used to remove a contact, refer to the ABAddressBook reference in the Apple’s iPhone Reference Library. You can download the reference at `http://developer.apple.com/iphone/library/documentation/AddressBook/Reference/ABAddressBookRef_iPhoneOS/ABAddressBookRef_iPhoneOS.pdf`.

## SUMMARY

In this chapter, you saw how you could easily integrate the various built-in applications into your own iPhone applications. In particular, you saw how you can invoke the built-in SMS, Mail, Safari, and phone dialer simply by using a URL string. You also learned about accessing the Contacts and Photo Library using the classes provided by the iPhone SDK.

## EXERCISES:

- 1. Name the various URL strings for invoking the Safari, Mail, SMS, and phone dialer applications.
- 2. What is the class name for invoking the Image Picker UI in the iPhone?
- 3. What is the class name for invoking the People Picker UI in the iPhone?

## WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Sending email from within your application | NSString *emailString = @"mailto:?to=USER@EMAIL.COM&subject=SUBJECT&body=BODY OF EMAIL"; [[UIApplication sharedApplication] openURL:[NSURL URLWithString:emailString]]; |
| Invoking Safari | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"http://www.apple.com"]]; |
| Invoking the Phone | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"tel:1234567890"]]; |
| Invoking SMS | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"sms:96924065"]]; |
| Accessing the Photo Library | Use the UIImagePickerController class and ensure your View Controller conforms to the UINavigationControllerDelegate protocol. |
| Accessing the Contacts application | Use the ABPeoplePickerNavigationController class from the AddressBookUI framework. |
