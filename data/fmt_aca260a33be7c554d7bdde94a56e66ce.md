
```objc
float playbackTime = i * duration/20;

[times addObject:[NSNumber numberWithFloat:playbackTime]];

}

[self.player
    requestThumbnailImagesAtTimes:times
    timeOption:MPMovieTimeOptionExact];
```

## 创建缩略图

在这里，我们首先直接从视频播放器获取视频的时长。⁴ 然后，在为 `MPMoviePlayer` 设置缩略图请求之前，我们确保已经注册了 `MPMoviePlayerThumbnailRequestDidFinishNotification` 通知，将任何此类通知重定向到 `playerThumbnailRequestDidFinish:` 方法，该方法我们将在稍后编写。

现在是时候设置缩略图请求了。记得 `requestThumbnailImagesAtTimes:` 方法接收一个我们想要获取缩略图的时间数组。由于我们的目标是创建 20 个缩略图，我们创建了一个 `NSMutableArray` 并迭代 20 次，每次根据分成 20 份的时长计算一个偏移量。然后我们使用数组调用 `requestThumbnailImagesAtTimes:`，并使用 `MPMovieTimeOptionExact` 时间选项表示我们希望缩略图尽可能接近时间码（用效率换取准确性）。因此，总结一下，我们等待播放器的元数据可用，并在此我们注册了接收缩略图通知，同时还获取了特定的异步请求，以从播放器视图创建 20 个缩略图。现在我们需要编写 `playerThumbnailRequestDidFinish:` 方法来在缩略图生成时对其进行处理。

## 处理缩略图

缩略图生成会产生一个通知，其中 `userInfo` 字典中包含两个我们感兴趣的项目：`MPMoviePlayerThumbnailKey` 的值是一个带有缩略图的 `NSNumber` 对象，而 `MPMoviePlayerThumbnailImageKey` 的值是缩略图本身。在代码中，我们检索这两个对象并使用辅助方法 `makeThumbnailImageViewFromImage:andTimeCode:` 创建一个图像，然后将其添加到 scroll view 中。

```objc
movieplayer/MoviePlayer4/Classes/MPMoviePlayerViewController.m
```

```objc
- (void)playerThumbnailRequestDidFinish:(NSNotification*)notification {

    NSDictionary *userInfo = [notification userInfo];

    NSNumber *timecode =
        [userInfo objectForKey:MPMoviePlayerThumbnailKey];

    UIImage *image =
        [userInfo objectForKey:MPMoviePlayerThumbnailImageKey];

}
```

- 4. 记得我们也可以从通知中检索播放器对象，就像我们在 132 页的代码中做的那样。

```objc
ImageViewWithTime *imageView =
    [self makeThumbnailImageViewFromImage:image andTimeCode:timecode];
```

```objc
[thumbnailScrollView addSubview:imageView];
```

你会注意到 `makeThumbnailImageViewFromImage:andTimeCode:` 方法返回的是一个 `ImageViewWithTime` 对象而不是标准的 `UIImageView`。这些类的唯一区别在于 `ImageViewWithTime` 有一个名为 `timecode` 的额外属性，用于将时间码直接与缩略图图像视图关联；正如你将要看到的，我们将在用户触碰缩略图时使用它。`makeThumbnailImageViewFromImage:andTimeCode:` 还处理了在滚动视图的帧（frame）中设置合适的位置，以便将其放置在滚动视图内。此时，你已经准备好再次构建并运行代码了。这一次，触碰缩略图将直接带你相应的视频内容（你可以在下一页的图 7.5 中看到我们的测试）。

![](img/06d76a71c379bfa5e6891245aa6bb22d_153_0.png)

```objc
(void)playerThumbnailRequestDidFinish:(NSNotification*)notification {

    NSDictionary *userInfo = [notification userInfo];

    NSNumber *timecode =
        [userInfo objectForKey:MPMoviePlayerThumbnailKey];

    UIImage *image =
        [userInfo objectForKey:MPMoviePlayerThumbnailImageKey];

}
```

```objc
ImageViewWithTime *imageView =
    [self makeThumbnailImageViewFromImage:image andTimeCode:timecode];
```

```objc
[thumbnailScrollView addSubview:imageView];
```

```objc
UITapGestureRecognizer *tapRecognizer =
    [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(handleTapFrom:)];

[tapRecognizer setNumberOfTapsRequired:1];
```

```objc
[imageView addGestureRecognizer:tapRecognizer];

[tapRecognizer release];
```

```objc
movieplayer/MoviePlayer4/Classes/MoviePlayerViewController.m

(void)handleTapFrom:(UIGestureRecognizer *)recognizer {

    ImageViewWithTime *imageView = (ImageViewWithTime *)recognizer.view;

    self.player.currentPlaybackTime = [imageView time floatValue];

}
```

`handleTapFrom:` 方法首先获取我们上的手势识别器（滚动视图中的一个图像视图），并将播放器的 `currentPlaybackTime` 设置为 `ImageViewWithTime` 存储的时间码。这将重置播放到时间码所在的视频内容。

## 7.6 展望

在本章中，你学习了基础：实例化 `MPMoviePlayerController` 并为视频渲染提供视图，检查视频播放属性，创建播放器状态通知的观察者，生成视频缩略图，甚至创建了一个简单的播放列表。

在下一章中，我们将进一步学习如何添加叠加在视频之上的视图，创建自定义播放控件，甚至查看全屏视频。最后，在之后的章节中，我们将学习流媒体视频内容。

![](img/06d76a71c379bfa5e6891245aa6bb22d_155_0.png)

图 7.5：带有视频播放器的缩略图视图

# 第8 章

# 高级视频播放器

在花费了整个章节研究 `MPMoviePlayerController` 之后，你现在掌握了许多关于控制播放器、从其获取状态信息以及在状态更改时接收通知的知识。你还知道如何为存储在设备本地的视频内容生成缩略图。

在本章中，我们将更进一步，通过为播放器添加交互性：首先是实现覆盖在视频之上的基于时间的消息，然后创建一套自定义的播放控制控件。随后，我们将通过探索全屏视频的处理来添加一些最后的润饰工作。

## 8.1 视频弹幕 (Video Shoutouts)

`MPMoviePlayerController` 的视图不仅可以播放内容。尽管你应该谨慎地处理此视图并且不要直接修改它的任何属性，但你可以添加自己的子视图（subviews），这为我们提供了在视频上层层内容的方法。

在本节中，我们将利用此功能创建一个简单的弹幕系统，允许我们在播放过程中的特定时间点显示视觉提示（callouts）——如果你见过 VH-1 风格的“弹出式”视频，你就知道我们要去哪里了（请查看下一页的图 8.1 预览）。为了这一目标，我们在 Movie5 项目中放置了一个 `CommentView` 类，它显示了一个思想气泡风格的图形，并配有透明度阴影和文本覆盖（如果你对代码感兴趣，可以尽管查看它，但它与我们这里的讨论稍微有点离题）：

![](img/06d76a71c379bfa5e6891245aa6bb22d_157_0.png)

在开始编写代码之前，请记住，我们的目标是演示如何向视频添加子视图，而不是实现一套维护弹幕文本和时间的复杂系统。事实上，我们关于弹幕的模型和逻辑可能被认为简单得令人尴尬。尽管如此简单，但让我们来看看这个模型：

```objc
movieplayer/MoviePlayer6/Classes/MovieViewController.m

-(void)viewDidLoad {

    [super viewDidLoad];

    shoutOutTexts = [[NSArray
        arrayWithObjects:
            @"This film rendered using\ncloud computing",
            @"Look out Frank, Rinky\nand Gamera!",
            nil) retain];
```

## 视频弹幕

```objc
shoutOutTimes = [[NSArray arrayWithObjects:[[NSNumber alloc] initWithInt:2],[[NSNumber alloc] initWithInt:325],nil] retain];

position = 0;

// rest的 viewDidLoad 放在这里

}
```

为了存储弹幕，我们使用了两个简单的数组：一个用于存储弹幕应该出现的时间码，另一个用于存储弹幕的文本。例如，我们可能会存储 "Hello Ma!" 和 17，以表示文本 "Hello Ma" 在视频播放 17 秒时显示。注意，我们还假设时间是有顺序的，较晚的时间在较早的时间之后。我们还添加了一个整数实例变量 `position`，我们设置它来跟踪此处（这里稍后我们会获取它），以跟踪当前的弹幕。

现在，为了知道何时显示弹幕，我们需要监控视频播放。为了做到这一点，让我们使用 `NSTimer` 类来设置每隔一段时间调用一次方法；在 `viewDidLoad` 方法中添加此代码，紧接弹幕数组实例化下方：

```objc
moviePlayer/moviePlayer5/Classes/MovieViewController.m

[NSTimer
    scheduledTimerWithTimeInterval:1.0f
    target:self
    selector:@selector(checkShoutouts)
    userInfo:nil
    repeats:YES];
```

我们正在使用 `NSTimer` 在一秒后调度方法调用，目标是类中的 `checkShoutouts` 方法。此外，我们希望这个定时器每秒重复执行该方法调用。

现在我们需要编写由定时器调用的 `checkShoutouts` 方法。它的工作原理如下：我们将维护一个实例变量 `position`，作为下一个要显示的弹幕的指针。每当定时器调用 `checkShoutouts` 方法时，我们将把播放器的当前 `currentPlaybackTime` 与当前弹幕时间进行比较，如果 `currentPlaybackTime` 等于或小于当前弹幕时间，我们将显示并增加 `position`。我们将时间比较逻辑将其抽象成一个名为 `timeForNextShoutout:` 的方法：

```objc
moviePlayer/Classes/MoviePlayerViewController.m

-(BOOL)isTimeForNextShoutout {

    int count = [shoutOutTimes count];

    if (position < count) {

        int timecode = [[shoutOutTimes objectAtIndex:position] intValue];

        if (self.player.currentPlaybackTime >= timecode) {

            return YES;

        }

    }

    return NO;

}
```

让我们使用这个方法来编写 `checkShoutouts`。首先，我们需要检查是否有新的弹幕要显示，如果是，我们将显示：

```objc
moviePlayer/Classes/MoviePlayerViewController.m

-(void)checkShoutouts:(NSTimer *)timer {

    if ([self isTimeForNextShoutout]) {

        CommentView *commentView = [[CommentView alloc] initWithText:shoutOutTexts[position]];

        [self.player.view addSubview:commentView];

        position++;

    }

}
```

等等，让我重新对齐逻辑。根据代码片段，它是这样的：

```objc
moviePlayer/Classes/MoviePlayerViewController.m

-(void)checkShoutouts {

    if ([self isTimeForNextShoutout]) {

        // 这里的逻辑

    }

}
```

实际上，为了操作，我们将移除：

```objc
moviePlayer/MoviePlayer5/MovieViewController.m

-(void)removeView:(NSTimer *)timer {

    UIView *view = self.commentView;

    [view removeFromSuperview];

}
```
