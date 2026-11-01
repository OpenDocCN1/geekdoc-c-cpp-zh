# WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Sending email from within your application | NSString *emailString = @"mailto:?to=USER@EMAIL.COM&subject=SUBJECT&body=BODY OF EMAIL"; [[UIApplication sharedApplication] openURL:[NSURL URLWithString:emailString]]; |
| Invoking Safari | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"http://www.apple.com"]]; |
| Invoking the Phone | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"tel:1234567890"]]; |
| Invoking SMS | [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"sms:96924065"]]; |
| Accessing the Photo Library | Use the UIImagePickerController class and ensure your View Controller conforms to the UINavigationControllerDelegate protocol. |
| Accessing the Contacts application | Use the ABPeoplePickerNavigationController class from the AddressBookUI framework. |