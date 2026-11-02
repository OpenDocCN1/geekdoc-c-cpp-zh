```
```objc
@property (nonatomic, retain) UITextField *body;

- (IBAction) btnSend: (id) sender;

@end
```
```

+   5. Back in Interface Builder, Control-click and drag the File’s Owner item to each of the three TextField views and select to, subject, and body, respectively.

+   6. Control-click and drag the Button view to the File’s Owner item and select `btnSend:`.

+   7. Insert the following code in bold into the EmailsViewController.m file:

```
```objc
#import "EmailsViewController.h"

@implementation EmailsViewController
@synthesize to, subject, body;

- (void) sendEmailTo: (NSString *) toStr
    withSubject: (NSString *) subjectStr
      withBody: (NSString *) bodyStr {

    NSString *emailStr =
        [NSString stringWithFormat:@"mailto:?to=%@&subject=%@&body=%@",
        [toStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding],
        [subjectStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding],
        [bodyStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding]];

    [[UIApplication sharedApplication] openURL:[NSURL URLWithString:emailStr]];
    [emailStr release];
}

- (IBAction) btnSend: (id) sender {
    [self sendEmailTo:to.text withSubject:subject.text withBody:body.text];
}

- (void) dealloc {
    [to release];
    [subject release];
    [body release];
    [super dealloc];
}
```
```

+   8. Press Command-R to test the application on a real iPhone. Figure 16-2 shows the application in action. After you have filled in the TextField views with the necessary information, click the Send button to invoke the Mail application and fill it with all the information you have typed in your application. Clicking the Send button in Mail sends the email.