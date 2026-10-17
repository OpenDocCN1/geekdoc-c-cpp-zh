
测试套件 '/Users/jnozzi/Library/Developer/Xcode/DerivedData/TestApp_Suite-gjvjpbtynoofyphkphrqcobvoibi/Build/Products/Debug/TestAppTests.octet(Tests)' 于 2011-04-13 20:02:20 -0400 启动
测试套件 'TestAppTests' 于 2011-04-13 20:02:20 -0400 启动
测试套件 'TestAppTests' 于 2011-04-13 20:02:20 -0400 完成。
执行了 0 个测试，0 个失败（0 个意外）在 0.000（0.000）秒内
测试套件 '/Users/jnozzi/Library/Developer/Xcode/DerivedData/TestApp_Suite-gjvjpbtynoofyphkphrqcobvoibi/Build/Products/Debug/TestAppTests.octet(Tests)' 于 2011-04-13 20:02:20 -0400 完成。
执行了 0 个测试，0 个失败（0 个意外）在 0.000（0.001）秒内
测试套件 'All tests' 于 2011-04-13 20:02:20 -0400 完成。
执行了 0 个测试，0 个失败（0 个意外）在 0.000（0.002）秒内

通常可以忽略前17行，因为它们与测试环境本身的成功或失败有关。如你在第11行（以“Test Suite...”开头的那一行）所见，测试套件启动和完成时会报告失败次数。

## 可导航的错误

测试所提供的不仅仅只是记录日志。遇到失败时，失败点会在源代码编辑器中作为错误高亮显示。图18.4显示了一个简单（但有点刻意）的测试，它断言 BOOL 值 YES 应等于 NO——这注定会失败。测试后，该失败被标记为一个问题，可以像其他问题一样进行导航。

同样有趣的是，问题导航器（图18.5）不仅忠实地显示测试失败，还显示失败性质的描述（基于你使用的断言类型），以及你提供的自定义消息（如果提供了的话）。

图18.4 编辑器中显示的测试错误

图18.5 问题导航器中显示的测试错误

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_297_0.png)

## 编写单元测试

图18.6 添加Person类

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_298_0.png)

要为TestApp创建一个恰当的说明性单元测试，你需要创建一些易于测试的内容，根据你已知必须可行的功能来设计测试，然后按照这些规范编写测试。在接下来的小节中，你将使用一个非常简单的Person类来完成这一工作。

### 创建可测试的内容

首先，向TestApp添加一个Person类。为此，从主菜单中选择 文件 > 新建 > 新建文件，向项目（TestApp目标）添加一个新的 Objective-C 类。将类命名为 Person，并使其成为 NSObject 的子类。保存前，务必确保新的 Person 类同时添加到 TestApp 和 TestAppTests 目标中（图18.6），以便它能够被你即将编写的测试用例使用。单击 Save 以添加该文件。

使用下面的代码构建一个基本的 Objective-C 类。将你的 Person.m 文件全部内容替换为以下代码：

```objective-c
#import "Person.h"

@implementation Person

- (id)init
{
    self = [super init];
    if (self)
    {
        firstName = nil;
        lastName = nil;
    }
    return self;
}

- (void)dealloc
{
    [firstName release];
    firstName = nil;
    [lastName release];
    lastName = nil;
    [super dealloc];
}

@synthesize firstName;
@synthesize lastName;

@end
```

然后，将你的 Person.h 文件的内容替换为以下代码：

```objective-c
#import <Foundation/Foundation.h>

@interface Person : NSObject {
    NSString * firstName;
    NSString * lastName;
}

@property (nonatomic, retain) NSString * firstName;
@property (nonatomic, retain) NSString * lastName;

@end
```

这段代码描述了一个基本的类，代表一个拥有名字和姓氏的人。假设你熟悉 Objective-C，你会意识到当 Person 第一次创建时，这两个 name 属性将为 nil。此外，这些属性的合成访问器允许将名字设置为 nil 或一个 NSString（可能为空）。这些是你应该避免的场景——一个人即使没有名字和姓氏，也应该始终具有名字和姓氏。为此，你需要设计一个测试。

### 设计测试

你的 Person 测试覆盖率目标很简单：所有 Person 实例都必须具有有效的名字和姓氏。也就是说，它们的名字或姓氏不能被设置为 nil 或空的 NSString，Person 实例也不能被初始化成这种状态。所有测试都必须包含在自己的方法中，并且必须以 `- (void)test...` 开头。

为了达到最低覆盖率，你需要四个测试：testLastNameCannotBeNil、testLastNameCannotBeEmptyString、testFirstNameCannotBeNil 和 testFirstNameCannotBeEmptyString。

你已经知道，在 Person 类当前状态下，这四个测试都会失败。目前没有任何代码来检查并强制执行这些要求。现在该编写测试了。

### 编写测试

为了编写测试，你需要向项目添加一个 Objective-C 测试用例类。你可以通过将一个 Objective-C 测试用例类从文件模板库拖到项目导航器中（在 TestAppTests 组下）来完成，如图 18.7 所示。

将类命名为 PersonTest.m，以便清楚地知道该测试属于哪个类。另外，仅将测试添加到 TestAppTests 目标（因为运行 TestApp 时不需要编译它）。你的设置应与图 18.8 类似。单击 Save。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_301_0.png)

图18.7 向项目添加测试用例类

图18.8 命名并配置测试用例类

将 PersonTest.m 的内容替换为以下代码：

```objective-c
#import "PersonTest.h"
#import "Person.h"

@implementation PersonTest

@synthesize personToTest;

- (void)setUp {
    [super setUp];

    // Create a person to test
    Person * newTestPerson = [[Person alloc] init];
    [self setPersonToTest:newTestPerson];
    [newTestPerson release];
}

- (void)tearDown {
    // Kill the test person
    [self setPersonToTest:nil];

    [super tearDown];
}

- (void)testLastNameCannotBeNil
{
    self.personToTest.lastName = nil;
    STAssertNotNil(self.personToTest.lastName, @"Last name cannot be nil!");
}

- (void)testLastNameCannotBeEmptyString
{
    self.personToTest.lastName = @"";
    STAssertTrue((self.personToTest.lastName.length > 0), @"Last name cannot be empty string.");
}

- (void)testFirstNameCannotBeNil
{
    self.personToTest.firstName = nil;
    STAssertNotNil(self.personToTest.firstName, @"First name cannot be nil!");
}

- (void)testFirstNameCannnotBeEmptyString
{
    self.personToTest.firstName = @"";
    STAssertTrue((self.personToTest.firstName.length > 0), @"First name cannot be empty string.");
}

@end
```

将 PersonTest.h 的内容替换为以下代码：

```objective-c
#import <SenTestingKit/SenTestingKit.h>

@class Person;

@interface PersonTest : SenTestCase {
    Person * personToTest;
}

@property (nonatomic, retain) Person * personToTest;

- (void)testLastNameCannnotBeNil;
- (void)testLastNameCannnotBeEmptyString;
- (void)testFirstNameCannnotBeNil;
- (void)testFirstNameCannnotBeEmptyString;

@end
```

### 验证测试

现在是时候确保你的测试能正常工作了。确保 TestApp scheme 处于活动状态，然后按 Command+U 或从主菜单中选择 产品 > 测试。执行后，你会得到四个预期的失败。它们会在编辑器中高亮显示，也会整齐地列在问题导航器中（图 18.10）。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_305_0.png)

图18.10 问题导航器中显示的预期失败

提示：你可以尝试在方案编辑器的 Test 操作面板中，取消选中相应测试旁边的 Test 复选框，从而禁用其中一个测试。再次运行测试，你会看到该失败从列表中消失，因为该测试没有被执行。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_305_1.png)

### 通过测试

为了通过测试，你的 Person 类显然需要防止 nil 或空白的名字。它不仅需要更智能的 setter 访问器，还需要在 -init 方法中提供一些默认值。将 Person.m 的全部内容替换为以下代码：

```objective-c
#import "Person.h"

@implementation Person

- (id)init
{
    self = [super init];
    if (self)
    {
        self.firstName = @"John";
        self.lastName = @"Smith";
    }
    return self;
}

- (void)dealloc
{
    [firstName release];
    firstName = nil;
    [lastName release];
    lastName = nil;
    [super dealloc];
}

- (NSString *)firstName
{
    return firstName;
}
```
