
```objc
ABRecordSetValue(person, kABPersonAddressProperty, address, nil);

//---add the address book for the contact and save the addressbook---
ABAddressBookAddRecord(addressBook, person, nil);
ABAddressBookSave(addressBook, nil);
CFRelease(person);
}
```

上述方法 - addContact，将联系人添加到通讯录应用程序。它使用以下信息填充联系人：

- 名字
- 姓氏
- 家庭地址
  - 街道
  - 城市
  - 州
  - 邮编
  - 国家
  - 国家代码

![](img/aab2d775c46f70cd606f2e58e2521324_404_0.png)

**图 16-11**

图 16-11 显示了已添加联系人的详细信息。

> **注意** 有关添加联系人所使用的各种方法的更多信息，请参阅 Apple 的 iPhone 参考库中的 ABAddressBook 参考。您可以在以下位置下载参考资料： http://developer.apple.com/iphone/library/documentation/AddressBook/Reference/ABAddressBookRef_iPhoneOS/ABAddressBookRef_iPhoneOS.pdf。

### 删除联系人

要从通讯录应用程序中删除联系人，请使用以下代码片段：

```objc
-(void) removeContact: (NSString *) firstName andLastName: (NSString *) lastName {

ABAddressBookRef addressBook = ABAddressBookCreate();
CFArrayRef allContacts = ABAddressBookCopyArrayOfAllPeople(addressBook);

CFIndex contactsCount = ABAddressBookGetPersonCount(addressBook);

for (int i = 0; i < contactsCount; i++)
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

前述方法 removeContact 接收两个参数 firstName 和 lastName，并搜索通讯录应用程序中具有匹配名字和姓氏的联系人。如果找到联系人，则将其从通讯录应用程序中删除。

> **注意** 有关删除联系人所使用的各种方法的更多信息，请参阅 Apple 的 iPhone 参考库中的 ABAddressBook 参考。您可以在以下位置下载参考资料： http://developer.apple.com/iphone/library/documentation/AddressBook/Reference/ABAddressBookRef_iPhoneOS/ABAddressBookRef_iPhoneOS.pdf。

### 摘要

在本章中，您了解了如何轻松地将各种内置应用程序集成到自己的 iPhone 应用程序中。特别是，您了解了如何仅使用 URL 字符串调用内置的 SMS、Mail、Safari 和电话拨号器。您还学习了如何使用 iPhone SDK 提供的类访问通讯录和照片库。

### 练习

1. 列出调用 Safari、Mail、SMS 和电话拨号器应用程序的各种 URL 字符串。
2. 在 iPhone 中调用图像选择器 UI 的类名是什么？
3. 在 iPhone 中调用人员选择器 UI 的类名是什么？

### 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| 在应用程序内部发送电子邮件 | `NSString *emailString = @"mailto:to=USER@EMAIL.COM&subject=SUBJECT&body=BODY OF EMAIL";`<br>`[[UIApplication sharedApplication] openURL:[NSURL URLWithString:emailString]];` |
| 调用 Safari | `[[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"http://www.apple.com"]];` |
| 调用电话 | `[[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"tel:1234567890"]];` |
| 调用短信 | `[[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"sms:96924065*"]];` |
| 访问照片库 | 使用 `UIImagePickerController` 类并确保您的视图控制器符合 `UINavigationControllerDelegate` 协议。 |
| 访问通讯录应用程序 | 使用来自 AddressBookUI 框架的 `ABPeoplePickerNavigationController` 类。 |

## 17 访问硬件

### 本章将学习的内容

- 如何从 iPhone 或 iPod Touch 获取加速度计数据
- 如何检测设备的摇动
- 如何使用 iPhone 和 iPod Touch 中的 Core Location 服务获取地理数据
- 如何在应用程序中显示地图

在上一章中，您了解了如何通过各种方式访问 iPhone 和 iPod Touch 上的内置应用程序——URL 字符串以及 iPhone SDK 提供的专用类。在本章中，您将学习如何访问设备的硬件，例如加速度计，并通过 GPS、蜂窝塔和无线热点获取位置信息。

### 使用加速度计

iPhone 和 iPod Touch 最具创新性的功能之一是内置加速度计。加速度计允许设备检测设备的方向并适应新的方向。例如，当您将设备横向旋转时，Safari 网页浏览器会自动将屏幕切换到横向模式，以便您现在拥有更宽的观看空间。同样，相机依靠加速度计来判断您是在竖屏还是横屏模式下拍照。

如果设备直立并快速向右移动，X 轴的值将从 0 增加到正值。如果快速向左移动，X 轴的值将从 0 减少到负值。如果设备快速向上移动，Y 轴的值将从 -1.0 增加到更大的值。如果设备快速向下移动，Y 轴的值将从 -1.0 减少到更小的值。

如果设备平放在桌子上然后掉落，Z 轴的值将从 -1.0 减少到更小的数字。如果向上移动，Z 轴的值将从 -1.0 增加到更大的数字。

> **注意** iPhone 和 iPod Touch 上使用的加速度计的最大读数为约 +/- 2.3G，分辨率为约 0.018 g。

在下面的试一试中，您将学习如何以编程方式访问加速度计返回的数据。获取加速度计数据可让您构建非常有趣的应用程序，例如水平仪，以及依赖于运动检测的游戏。

### 试一试 访问加速度计数据

代码文件 [Accelerometer.zip] 可在 Wrox.com 下载

1. 使用 Xcode 创建一个新的基于视图的应用程序项目，并将其命名为 Accelerometer。
2. 双击 AccelerometerViewController.xib 文件在 Interface Builder 中编辑它。
3. 使用六个标签视图填充视图窗口，如图 17-2 所示。
4. 在 AccelerometerViewController.h 文件中，添加以下以粗体显示的语句：

```objc
#import <UIKit/UIKit.h>

@interface AccelerometerViewController : UIViewController <UIAccelerometerDelegate> {
    IBOutlet UILabel *labelX;
    IBOutlet UILabel *labelY;
    IBOutlet UILabel *labelZ;
}

@property (nonatomic, retain) UILabel *labelX;
@property (nonatomic, retain) UILabel *labelY;
@property (nonatomic, retain) UILabel *labelZ;

@end
```

![](img/aab2d775c46f70cd606f2e58e2521324_410_0.png)

5. 返回 Interface Builder，Control-单击并拖动 File's Owner 项到每个标签视图，并分别选择 labelX、labelY 和 labelZ。
6. 在 AccelerometerViewController.m 文件中，添加以下以粗体显示的语句：

```objc
#import "AccelerometerViewController.h"

@implementation AccelerometerViewController

@synthesize labelX, labelY, labelZ;

- (void)viewDidLoad {
    UIAccelerometer *acc = [UIAccelerometer sharedAccelerometer];
    acc.delegate = self;
    acc.updateInterval = 1.0f/60.0f;
    [super viewDidLoad];
}

- (void)accelerometer:(UIAccelerometer *)acc didAccelerate:(UIAcceleration *)acceleration {
    NSString *str = [[NSString alloc] initWithFormat:@"%g", acceleration.x];
    labelX.text = str;
    str = [[NSString alloc] initWithFormat:@"%g", acceleration.y];
    labelY.text = str;
    str = [[NSString alloc] initWithFormat:@"%g", acceleration.z];
    labelZ.text = str;
    [str release];
}

- (void)dealloc {
    [labelX release];
    [labelY release];
    [labelZ release];
    [super dealloc];
}
@end
```

7. 按 Command-R 在 iPhone 设备上测试应用程序。图 17-3 显示了当我的 iPhone 放在 iPhone Dock 底座上时应用程序显示的数据。

> **注意** 对于加速度计数据，您需要一个真实设备——iPhone 或 iPod Touch。
