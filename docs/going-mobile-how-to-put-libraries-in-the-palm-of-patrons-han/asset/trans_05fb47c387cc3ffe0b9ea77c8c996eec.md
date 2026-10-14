

## 7 超越基础

本书的目的是让构建应用尽可能简单。你可以向应用中添加 JavaScript 使其更炫，但详细讨论 JavaScript 会偏离本书的初衷——保持简单。

JavaScript 是一种相当强大的语言，可以做很多事情，但学习它并不是构建一个外观出色的应用所必需的。如果你懂 JavaScript，就用它；如果你不懂，还有另一种选择：小部件。如果你写博客或阅读博客，那么你很可能已经对小部件了如指掌，即使你不以这个名字称呼它们。小部件是那些坐在博客侧边栏上的小方块，提供指向 Twitter、Facebook 和 Google 新闻流等内容的链接。小部件表面上看起来很简单，但每个小部件内部都有成页的代码。好消息是，你不必了解代码也能构建它们。

对“widgets”进行一次简单的网络搜索，就会找到数千个提供可定制小部件的页面；有些是免费的，有些则附带少量费用。你需要提防使用 Flash 的小部件（目前许多手机不支持，尤其是 iPhone）。

许多网站也提供小部件。Twitter 是完美的例子。在 Twitter 的小部件网页（https://twitter.com/widgets/）上，你只需几步就能构建一个自定义小部件。

首先，在小部件页面上，选择 My Website（图 7.1）。

![](img/1c33fb3bae0a705f04846bc77d279fd7_48_0.png)

在下一页你会看到几个选项；选择 Profile Widget，它将显示你图书馆最近的推文。

接下来，你可以自定义你的小部件（图 7.2）。在用户名下，理想情况下应填写你图书馆的名称，但你也可以填写作者、杂志或任何其他拥有公开 Twitter 账号的人的名字。这可以在你没有时间亲自操作时为你的应用提供内容。

![](img/1c33fb3bae0a705f04846bc77d279fd7_49_0.png)

**图 7.2**

在 Preferences 下，你可以选择显示多少条推文。虽然 Twitter 的限制是三十条推文，但最好考虑你正在为其开发的移动设备的屏幕尺寸。你不希望用户滚动太多——理想情况下，你根本不希望他们滚动。因此，你可能将显示的推文数量保持在四条。

在 Appearance 下，确保你选择的颜色与你的应用颜色相匹配。在 dimensions 下，你可以将其调整为手机的尺寸，或选择 auto width 以使其自动调整小部件本身的大小。

最后，滚动到页面底部并选择 Finish & Grab Code（图 7.3）。现在只需复制代码并粘贴到你的应用代码中即可。

![](img/1c33fb3bae0a705f04846bc77d279fd7_49_1.png)

**图 7.3**

如果你正在考虑提供基于聊天的参考服务（如果你没有考虑，你应该考虑——不这样做，你将错过整整一代用户），那么可以考虑 LibraryH3lp（http://libraryh3lp.com）。该网站的服务有少量年度费用（根据你所在城市的大小而有所不同），但比许多类似服务便宜得多。Meebo 和 Google Talk 提供免费的聊天服务，但它们的小部件使用 Flash，因此在 iPhone 应用中不受支持。相比之下，LibraryH3lp 使用 Java，因此对应用友好。框 4 显示了 LibraryH3lp 小部件的源代码。

在移动浏览器中，框 4 中的代码看起来类似于图 7.4。

Widgetbox（www.widgetbox.com）是最受欢迎的小部件构建器之一；它是免费的但由广告支持。还提供无广告的专业版，年费从 $29.99 起。该网站提供基于 Flash 和基于 Java 的小部件。

Facebook 也提供了将个人资料嵌入网站的步骤（http://developers.facebook.com/docs/guides/web/）。然而，Widgetbox 制作了一个更用户友好的版本，如果你刚开始开发，它是更好的选择。只需确保你复制的是基于 Java 的小部件版本，而不是基于 Flash 的版本。

### 框 4 ■ LibraryH3lp 小部件的源代码

```html
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<meta http-equiv=content-type content="text/html; charset=UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0 user-scalable=yes" />
<title></title>
<link type="text/css" rel="stylesheet" href="/css/mobile.css" />

<style id="dynamic" type="text/css">
</style>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js"></script>
<script type="text/javascript" src="http://d1aaqh87bn7fin.cloudfront.net/mobile_2010011801.min.js"></script>
<!--
<script type="text/javascript" src="/js/lib/strophe.js"></script>
<script type="text/javascript" src="/emoticons/emoticons.js"></script>
<script type="text/javascript" src="/js/mobile.js"></script>
-->
</head>
<body>
<div id="header">
<img id="presence" src="/presence/image/simpletext/unavailable" />
<h1 id="title"></h1>
</div>

<div id="to" jid="my-queue@chat.libraryh3lp.com" lang="en"></div>
<div id="recv"></div>
<div id="send">
<form action="#" method="post" onSubmit="return false;">
<textarea id="msg">chat requires javascript...</textarea>
</form>
<div id="buttons"><a href="#" onclick="libraryh3lp.sendLine(); return false;"><img height="42" width="30" src="/images/mobilesend.png" /></a></div>
</div>
<div id="status"><a id="mail" href="#" onclick="libraryh3lp.mailTranscript(); return false;">Email transcript</a></div>
</body>
</html>
```

![](img/1c33fb3bae0a705f04846bc77d279fd7_51_0.png)

**图 7.4**

Widgetbox 也使开发移动应用变得容易（www.widgetbox.com/mobile/）。如果你想要一个基本的移动网页应用（不是原生应用）来显示 Twitter、Facebook 或 Flickr 更新，那么 Widgetbox 可能很适合图书馆；然而，它不允许用户编辑源代码，你可能会很快发现它对你的图书馆来说过于受限。

Widgipedia（www.widgipedia.com）是寻找小部件的另一个很好的资源；然而，它们是用户提交的并且可定制。

PhoneGap 提供了开发人员可以复制用于其自身应用的几段代码；你可以在网站的 Community 部分找到这些代码（www.phonegap.com/community/）。它经常更新，所以经常回来查看。一个有用的代码是基于手机 GPS 的地图包含（http://phonegap.pbworks.com/PhoneGap-Geolocation-Sample-Application）。

我已经测试了本章中的所有小部件和工具，以确保它们能与 iPhone 应用配合使用。正如我之前所说，JavaScript 在移动网页应用和原生应用上很棘手，所以在实施前务必测试。对于我在原生 iPhone 应用上成功测试的每一段 JavaScript，就有十几段返回错误。

## 其他移动方式

本书的目的是向图书管理员展示开发移动应用可以有多简单。在很大程度上，移动应用运行在智能手机上。然而，图书管理员也可以主动调查其他移动应用程序编程接口（APIs）。

Foursquare（有关文档信息，请参阅 http://groups.google.com/group/foursquare-api/web/api-documentation/），有些人称其为下一个 Twitter，是一款基于位置的社交媒体应用，允许人们告诉朋友他们确切的位置，并成为他们经常访问的地点“市长”。Gowalla（http://gowalla.com）是另一个像 Foursquare 一样的社交网站，越来越受欢迎；与 Foursquare 不同的是，Gowalla 在定制方面提供了更多。

在思考移动应用时，图书馆应尽可能多地考虑免费技术用于推广——Foursquare 和 Yelp 已经拥有你可以轻松链接的应用。如果你的图书馆尚未在 Foursquare 上占领自己的位置，为什么不呢？这是一个完美的推广渠道——人们可以用图书馆应用签到图书馆并获得免费的东西——免费视频、减免罚款、小奖品等等。

在手机上运行最好的社交媒体网站，与在网络上最受欢迎的网站相同：Facebook、Twitter、YouTube 和 Flickr。如果你的图书馆还没有 Facebook 粉丝页，现在是时候了。这对其他三个也同样适用，尽管程度较轻。有什么比用视频和照片展示你的图书馆活动更好的方式呢？所有社交媒体网站的优点在于它们相互集成——你可以将 Twitter 更新推送到 Facebook，并即时在 Twitter 和 Facebook 上分享 YouTube 视频和 Flickr 幻灯片。这些网站最好的地方是，你不需要做任何事情就能实现移动化。如果你有 Twitter 或 Facebook 页面，它已经是移动兼容的——不需要额外步骤。

图书管理员不会给你答案——他们只是为你指明方向。你的应用也应如此。通过找到已经完成的代码，节省你自己的时间和麻烦。我希望你决定开发一个移动应用，但至少，我希望你确保你的图书馆积极参与这里提到的移动技术。

