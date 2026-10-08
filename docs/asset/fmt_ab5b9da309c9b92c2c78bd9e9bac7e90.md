
决定浏览会话是否使用 HTTPS 的因素是通信的 Web 服务器是否配备了一个名为“证书”的特殊文件。在提供加密通信的背景下，每当 Alice 与银行开始 Web 会话时，证书被用于创建一个唯一的加密密钥。每个使用 HTTPS 的网站都有一个唯一的证书，可以将证书视为创建加密密钥的许可。事实证明有多种类型的证书。证书之间的区别之一在于证书是否由注册的证书颁发机构签名（即验证）并购买——证书费用大约为每年数百美元。网络浏览器知道证书颁发机构的身份，如果网站拥有由注册的证书颁发机构签名的证书，那么就知道网站所有者是从信任源购买的证书。网站还可以拥有自签名证书，这种证书不是购买的，而是由网站所有者创建的。这允许网络浏览器使用 HTTPS，但没有提供与签名证书同水平的保证。如果用户正在浏览的网站尝试使用自签名证书创建 HTTPS 连接，大多数网络浏览器都会向用户警告。由于自签名证书被认为是不不可信的，遇到使用自签名证书的合法网站是非常罕见的现象。图 7.11 显示了证书示例，图 7.12 显示了浏览器将用于指示存在自签名证书的消息类型。

图 7.11 显示了 Gmail 拥有的证书信息。在这个示例中，注册的证书颁发机构 Thawte 已经验证了该证书。该图还显示了一些虽然不是证书的一部分但仍然很有趣的信息。还可以看到该网站被访问的次数以及网站是否在计算机上放置了 cookie。该图还显示了保存密码的存在，这是第 3 章中讨论过的话题。图 7.12 显示了如果访问带有自签名证书的网站会发生什么。正如消息明确的那样，因为无法通过信任的机构验证网站身份，因此不应接受该证书。除非你绝对信任正在访问的网站，否则几乎没有理由去接受自签名证书，这样做可能会导致机密信息的丢失。

![](img/785c52f93de89c98051552f6701d2efd_195_0.png)

图 7.11 证书信息。

![](img/785c52f93de89c98051552f6701d2efd_195_1.png)

图 7.12 自签名证书警告。

鉴于 HTTPS 的基本假设，经常会出现几个问题。

### 问题 1：如果 HTTPS 缓解了窃听，为什么不是每个网站都使用它？
这个问题有两个答案；第一个与成本有关，第二个是对于许多网站来说，增加的安全性并非必要的。加密每个客户端与给定 Web 服务器之间的网络流量需要额外的计算，因此会以时间为代价。因为与网站的每次交互都需要加密然后可以解密，客户端可能会遇到较慢的加载时间，从而导致特定网站的体验较差。此外，引向下一个问题的答案是，如果网站内容不需要加密，那么购买证书可能是一种不必要的成本。这是另一个安全性与便利性冲突的例子。

关于是否每个网站都使用 HTTPS 的问题的后部分答案是，许多网站不需要它。对于许多站点来说，信息是公开的，没有敏感数据需要保护。然而，对于任何处理敏感用户信息的网站（如银行或医疗），HTTPS 是必不可少的。

### 问题 2：如何判断网站是否正在使用 HTTPS？
网络浏览器有不同的方式来指示它们正在使用 HTTPS。长期以来，网络浏览器在窗口角上显示锁图标。最近，网络浏览器采用了基于颜色的方案，通过控制 favicon 的颜色来指示 HTTPS 的安全性。由于缺乏标准，某些浏览器仍然使用锁作为 HTTPS 连接的视觉指示，某些则同时使用锁和 favicon 颜色指示来表示使用 HTTPS。

图 7.13–15 显示了 Firefox 和 IE（Internet Explorer）网络浏览器不同 HTTP/HTTPS 安全水平的地址栏示例。图 7.13 使用 HTTP 且不任何加密级别的地址栏说明。除了 URL 中的 HTTP 协议外，可以通过 favicon 缺少颜色指示和缺少闭合锁进一步确认未加密连接。图 7.14 中的下一组示例显示了当浏览器连接到具有标准签名证书的 Web 服务器时的 HTTPS 地址栏。可以看到 Firefox 浏览器的 favicon 区域是蓝色的，而 IE 地址栏没有使用类似的颜色作为指示。与 Firefox 不同，IE 还显示了闭合锁来表示 HTTPS。

![](img/785c52f93de89c98051552f6701d2efd_197_0.png)

图 7.13 HTTP（无颜色 + 无锁 = 非 HTTPS）

![](img/785c52f93de89c98051552f6701d2efd_197_1.png)

图 7.14 HTTPS（蓝色或闭合锁 = 标准 HTTPS）

![](img/785c52f93de89c98051552f6701d2efd_197_2.png)

图 7.15 扩展验证 HTTPS（绿色 = EV HTTPS）

# 安全地浏览全球维网 173

一个 HTTPS 连接。在第三个示例中，图 7.15 展示了两个具有绿色图标（IE 也有锁头图标）的 HTTPS 连接，这表示已使用扩展验证（EV）证书建立了 HTTPS 连接。与带有标准证书的网站（即蓝色图标或锁头）相比，拥有 EV 证书的网站（即绿色图标）已经完成了额外的身份验证过程，并支付了溢价费用获取此类证书。EV 证书背后的动机是为网络注入更多信任。因此，当 Alice 访问带有 EV 证书的网站时，她可以更有信心自己确实正在与信誉良好的网站进行通信。

为什么网站同时使用 HTTP 和 HTTPS？通过你的浏览体验，你可能注意到某些网站在单次浏览会话中同时使用了 HTTP 和 HTTPS。

# 174 ■ 安全素养 在数字世界中保持安全

出于性能考虑，某些网站仅使用 HTTPS 来验证用户（即对用户名和密码的交换进行加密），然后在与网站的剩余交互中默认回到 HTTP。如之前讨论的，对每个请求进行加密和解密需要额外的时间，从而缩短了网页加载时间。在过去，许多网络端电子邮件提供者都有过这种做法。网站会使用 HTTPS 安全地验证用户，但一旦登录，网站就会恢复到 HTTP。在这种背景下，使用 HTTP 既是安全风险也是隐私风险，因为它允许嗅探所有的邮件通信——这些信息通常是人们认为是隐私和机密的信息。作为回应，许多网络端电子邮件提供者现在为其客户的整个邮件会话默认提供 HTTPS 加密，以防止窃听威胁。通常，网络端电子邮件账户允许用户在偏好设置中选择“始终使用 HTTPS”选项。在浏览网页时，应尽可能使用 HTTPS，以防止隐私和机密信息的泄露。

## 7.4 浏览器历史

Cookies 和密码不是网页浏览器存储的唯一类型信息。为了提供更方便的浏览体验，网页浏览器会存储许多其他类型的信息。根据你个人的观点，存储此类信息可能会侵犯个人隐私。其中一种信息（如之前第 7.2.1 节所述）是网页浏览器通常存储网页的元素（如文本和图片），这样在再次访问同一网站时，浏览器就无需再次下载相同的内容。这一功能被称为浏览器缓存，旨在加快网络的使用速度。图 7.16 显示了浏览器缓存中存储的项目示例。

![](img/785c52f93de89c98051552f6701d2efd_199_0.png)

```
Number of entries: 47500
Maximum storage size: 1048576 KiB
Storage in use: 320630 KiB
Cache Directory: C:\Users\...AppData\Local\Mozilla\Firefox\xxxx.default\Cache\nCache Entry
```

图 7.16 缓存示例。

图 7.16 显示浏览器缓存（即磁盘缓存设备）有 47,300 个条目，图 7.17 显示了图 7.2 所示示例中缓存的两个条目。如所见，缓存保存了图片以及下载图片的日期和时间，并进一步指示了图片从缓存中删除之前的剩余时间。从用户的角度来看，如果有人访问了你的计算机，这些保存的文件可能会带来隐私问题。访问网页的简单行为会在浏览器中留下痕迹，其持续时间可能比预期的要久得多。

除了缓存，网页浏览器还具有记忆访问过的网站 URL 的能力。这通常被称为自动补全，可以在图 7.18 中看到其说明。在这个示例中，用户在地址栏中输入了“www.esp”，浏览器通过列出与输入匹配的之前访问过的 URL 列表做出响应。

浏览器提供的另一个功能是“自动填充”网页内的文本字段。与网页地址栏的自动补全功能类似，自动填充通过提供用户已输入过的项目列表来填充网站上的文本字段的服务（图 7.19）。这些信息的每种类型都由网页浏览器保存，旨在加速或简化你的浏览体验。

| http://www.img.net/images/fish.jpg | 100860 bytes | 2 | 2011-07-21 03:55:59 | 2011-07-26 00:46:48 |

| http://iac.iasstate.edu/images/morefish.jpg | 23961 bytes | 1 | 2011-07-21 08:55:59 | 2011-07-30 22:29:38 |

图 7.17 存储在计算机上的缓存图片。

![](img/785c52f93de89c98051552f6701d2efd_200_0.png)

图 7.18 Web 地址自动补全。

# 安全素养：在数字世界中保持安全

![](img/785c52f93de89c98051552f6701d2efd_201_0.png)

图 7.19 文本字段自动填充。

除了在私人计算机上使用浏览器的隐私考虑外，在公共计算机上使用浏览器还有许多相关问题。当你不希望下一个使用共享计算机的人通过浏览器积累关于用户行为的“数字面包屑”来了解你的活动时，就会出现这种情况。防止私有或共享计算机的后续用户了解你的活动的方法有两种主要方法；同样的方法也可用于防止或删除跟踪 Cookie。首先，网页浏览器允许你在在使用浏览器后“清除所有历史”。如图 7.20 所示，执行此操作将

![](img/785c52f93de89c98051552f6701d2efd_201_1.png)

图 7.20 清除所有浏览器历史。

![](img/785c52f93de89c98051552f6701d2efd_202_0.png)

**7.21** 限制浏览器历史。

删除浏览器的所有历史，包括 Cookie、缓存和表单搜索历史。第二种选择是限制或防止浏览器在你浏览时记住关于你操作的信息。例如，在图 7.21 中，可以通过勾选“永久隐私浏览模式”复选框防止 Firefox 浏览器记住任何个人信息，或者选择自定义设置来防止使用 Cookie 或下载历史等单个组件。除了这些控制外，许多流行的浏览器还允许用户在“隐私浏览模式”下上网。正如附录 C（网络浏览技术）中更详细讨论的那样，隐私浏览模式防止浏览器记住用户的操作。

## 7.5 总结

由于计算机对万维网的普遍使用和依赖，攻击者花费了大量尝试利用与使用网络相符的人为技术漏洞。这些攻击的核心关注点是浏览器以及为了让网络体验更丰富、方便、交互和及时而提供的功能。这些许多特性具有严重的安全和隐私影响。理解浏览器如何工作、安全与隐私的权衡，以及支持网络使用的安全特性和限制，对于计算机安全的目标至关重要。

# 178 ■ 安全素养 在数字世界中保持安全

- 通过 HTML 标签的使用，图片和链接都可以被用来欺骗用户认为电子邮件或网页的内容是真实的，而实际上却是钓鱼邮件或网页。
- 除了显示简单的文本和图片，网页浏览器还具有播放视频音频、执行多种脚本以及打开大量文档的能力。与其他类型的软件一样，每个执行代码的浏览器功能都容易受到利用软件漏洞的恶意代码的影响。
- 请求网页的简单行为会导致恶意软件的静默下载。
- 浏览器 Cookie 允许网站跟踪用户操作，从而为浏览器交互提供状态或历史。
- 除了 Cookie 中存储的信息外，这些信息在互联网上的记录、共享和传输也存在许多安全和隐私问题。
- 浏览器 Cookie 的体现了安全/隐私与便利性之间的权衡。
- HTTPS 通过加密请求计算机与相应 Web 服务器之间的流量，缓解了窃听威胁和机密性丢失。
- 尽管并非所有网络交易都需要使用 HTTPS，但在互联网上提交隐私或机密信息时应尽可能使用 HTTPS。
- 网站使用 HTTPS 并不保证该网站合法或安全。网络犯罪分子同样可以购买证书来创建 HTTPS 网站。
- HTTPS 不能防止键盘记录器、恶意软件或黑客攻击。

# 安全浏览万维网 — 179

- Cookies、缓存图像、表单和搜索历史、浏览历史以及记住的密码都提供了便利，但也带来了安全和隐私风险。

## 参考文献

Andrews, M., and Whittaker, J.A. 2006. How to Break Web Software: Functional and Testing of Web Applications and Web Services. Boston: Addison-Wesley Professional.

Angwin, J. 2010. The web's new gold mine: secrets. Wall Street Journal. http://online.wsj.com/article/SB100014240527487039409045739507325984904.html (访问于2012年4月30日)。

AWPG. 2012. Consumer advice: how to avoiding phishing scams. http://www.anti-phishing_recs.html (访问于2012年4月30日).

Ceruzzia, P.E. 2003. A History of Modern Computing. Cambridge, MA: MIT Press.

Deans, P. 2009. Social Software And Web 2.0 Technology Trends. Idea Group Inc.

Garfinkel, S., and Spafford, G. 2001. Web Security, Privacy and Commerce. Sebastopol, CA: O'Reilly Media.

Gobel, J.G., and Dewald, 2010. Client- Honeypots: Exploring Malicious Websites. Munich, Germany: Oldenburg Verlag.

Courley, D., and Totty, B. 2002. HTTP: The Definitive Guide. Sebastopol, CA: O'Reilly Media.

Governor, J., Nickull, D., and Hincliffe, 2009. Web 2.0 Architectures. Sebastopol, CA: O'Reilly Media.

Howard, R. 2010. Cybersecurity Essentials. Boca Raton, FL: CRC Press.

Jones, R. 2015. Internet Forensics. Sebastopol, CA: O'Reilly Media.

Morley, D., and Parker, C.S. 2010. Understanding Computers: Today and Tomorrow, Introductory. Independence, KY: Cengage Learning.

Oppringer, R. 2009. Ssl and Tis: Theory and Practice. Norwood, MA: Artech House.

Parsons, J.J., and Oja, D. 2010. Practical PC. Independence, KY: Cengage Learning. Pleefer, C., and Pleefer, S.L. 2011. Analyzing Computer Security: A Threat/Vulnerability/Countermeasure Approach. Indianapolis, IN: Prentice Hall

Realtimepublishers, and Sullivan, 2005. The Definitive Guide to Controlling Malware, Spyware, Phishing, and Spam. San Francisco, CA: Realtimepublishers.com.

Shafer, S.M. 2011. HTML, XML, and CSS Bible. New York: Wiley, Inc. Shelby, G.B., Woods, D.M. and Morin, W.J. 2010. HTML, XML, and CSS: Comprehensive. Independence, KY: Cengage Learning.

Sydell, L. 2010. Smart cookies put target online ads on the rise. National Public Radio. http://www.npr.org/templates/story/story.php?storyId=130349989 (访问于2012年4月30日)。

Zimmer, M.T. 2007. The Quest for the Perfect Search Engine: Values, Technical Design, and the Flow of Personal Information in Spheres of Mobility. Ann Arbor, MI: ProQuest.

# 上线购物

## 8.1 引言

当臭名银行大盗威利·萨顿（Willie Sutton）被问及为什么要抢劫银行时，他回答道：“钱在那儿。”在线世界的银行大盗就是网络犯罪分子。然而，与银行大盗不同，网络犯罪分子行劫的目标是获取个人、机密和财务信息（为了简洁起见，本章将所有此类信息称为“财务信息”）。随后，网络犯罪分子通过直接使用信息或在地下市场出售，将这些财务信息转化为利润。
