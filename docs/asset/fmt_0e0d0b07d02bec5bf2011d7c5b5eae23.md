
`sudo` 允许临时超级权限，但不应用于此操作。

输入登录密码，这是登录设备时密码。

选择挂载密码。

再次输入挂载密码。

`ecryptfs-setup-private` 脚本创建 `/home/user/Private` 目录并测试加密挂载是否符合预期。

重启设备后，在 `/home/user/` 下将有一个加密目录，可以存储所有机密信息。

> Ubuntu 的自动无密码登录意味着 `~/Private` 目录默认未挂载。设计如此，意味着当点击 `~/Private` 目录时需要输入密码。完成后，加密数据即可供用户使用。

应使用不同的密码来加密挂载；这只有在需要手动恢复数据时才是必要的。

## 实际示例

然而，OpenOffice 可能会消耗大量资源，这在移动设备上可能是一个问题。由于 Ubuntu MID 团队编写了一个名为 Trechet (treb) 的应用程序，它是一个用于办公文件的处理器。

treb 是一个读取由 Microsoft Office 应用创建文档的接口。它通过使用 OpenOffice 作为过滤器将文件转换为 PDF，并启动 Evince 来查看结果。在 Evince 关闭后，临时 PDF 文件将被删除，treb 本身也会关闭。

treb 作为 MID 安装的一部分提供，也可以使用 `apt-get` 安装；可以从命令行运行以显示图 6-1 所示的 GUI。

![](img/001c747b841ab338ed35c50dbdd0c933_166_0.png)

图 6-1

```bash
$ apt-get install treb

$ treb
```

## 多媒体用户

为多媒体用户组提供设备的供应商拥有一个从当前智能手机市场发展而来的预存在且现成的市场。尽管多媒体通常与图像、文本相关，但它也可以指整合了广泛兴趣数据的应用程序。移动设备上最知名且最流行的应用程序可能是 Canola。它是使用 Python 和 Enlightenment Foundation Libraries (EFL) 构建的，并使用插件系统来启用 YouTube、Flickr 等。Google Summer of Code 2009 有一些项目被批准，用于为 Twitter、Remember the Milk 甚至一个 IM 客户端创建插件。

EFL 在第 4 章中有更详细介绍。

另一个可用的解决方案是名为 Entertainer 的媒体中心。它旨在为 Gnome 和 XFCE 环境提供一个简单易用的应用程序。Entertainer 完全用 Python 编写，并使用 GStreamer 的多媒体框架进行多媒体播放。用户界面使用 Clutter 库实现。

Clutter 在第 4 章中有更详细介绍。

# 第 6 章：应用程序选择

## 实际示例

Entertainer 还包含一个私人视频录制器，这意味着它可以用于观看电视并录制节目供以后观看。要安装 entertainer，将 entertainer PPA 添加到 `/etc/apt/sources.list`：

```text
deb http://ppa.launchpad.net/entertainer-releases/ppa/ubuntu jaunty main
deb-src http://ppa.launchpad.net/entertainer-releases/ppa/ubuntu jaunty main
```

然后执行：

```bash
$ sudo apt-get update && sudo apt-get install entertainer
```

还将 GPG 密钥添加到您的软件源认证中（系统 ⇩ 管理 ⇩ 软件源 ⇩ 认证）。选择“导入密钥文件...”并添加在 entertainer 页面找到的密钥。

然后运行内容管理器并选择设备上的某些媒体文件夹或提供 URL：

```bash
$ entertainer-content-manager
```

内容管理器的界面类似于图 6-2。

![](img/001c747b841ab338ed35c50dbdd0c933_167_0.png)

图 6-2

接下来，运行前端：

Ubuntu Netbook Remix 上的 Entertainer 看起来像图 6-3。

![](img/001c747b841ab338ed35c50dbdd0c933_168_0.png)

图 6-3

退出 Entertainer 请按 `Q` 键。接下来将解释其他有用的键命令。

### Entertainer GUI 中的常用快捷键绑定

Entertainer 通过键盘控制，如下：

- `F` — 切换全屏开启/关闭。
- `P` — 在视频或音频播放时切换暂停/播放。
- `S` — 停止播放。
- `H` — 导航到主屏幕；在任何地方按此键都会显示主菜单。
- `I` — 在全屏模式下切换信息。
- `1`, `2`, `3`, `4` — 更改视频宽高比例。
- 方向键 — 导航菜单。
- `Enter` — 选择菜单项。
- `Backspace` — 导航到上一个屏幕。

## 社交网络用户

这一市场群体有时被营销人员称为 Y 代（Gen Y）（这是 X 代术语的延续，通常被理解为出生在 20 世纪 80 年代和 90 年代的人）。这显然是一个巨大的市场，对设备制造商和 ISV 具有很大的吸引力。该群体的人对互联网非常熟悉，特别是在 Facebook、Twitter 和 MySpace 等社交网络上。由 Junco 和 Jeanna Mastrocisca 在其书籍《连接网络：高等教育专业人员需要了解的现状》中对美国 707 名大学生进行的调查显示，同认同是一个关键动力。该调查的其他有趣点是：

- 97% 拥有电脑。
- 97% 使用对点传输下载过音乐和其他媒体。
- 94% 拥有手机。
- 76% 使用社交网络网站。
- 75% 的大学生拥有 Facebook 账号。
- 60% 拥有某种类型的便携移动设备。

## 位置感知型用户

家有年迈父母和幼儿的用户认为“位置”概念对他们非常重要。这组用户的可用收入也较高，因为他们已经工作多年，因此对 OEM 来说是一个很有吸引力的市场。用户对位置感知移动设备的通用期望包括：

- 自动重新配置的能力，使其始终使用正确的网络设置（用于防火墙和 VPN），并打印到正确的打印机（即：在家里使用家用打印机，在办公室时使用工作打印机）
- 安全性，仅允许指定的物理位置访问
- 帮助查找丢失或被盗的设备
- 能够轻松与房间内的其他人共享电源或演示文稿，而无需通过电子邮件发送或在公共服务器上设置文件夹

这些功能的一部分可以使用运行在设备本地的简单 Web 界面呈现给用户。

# 实际示例

在本节中，你将学习如何为 MID（多媒体设备）创建一个支持 GPS 的独立 Web 应用。它使用 Python 应用嵌入了 Web 服务器和数据库，并通过 XML-RPC 从 D-Bus 接口接收信息。它使用了 Django Web 应用框架。

D-Bus 将在第 4 章中详细介绍。

## 背景

传统上，Debian 类系统使用一个名为 `gpsd` 的守护进程提供 GPS 服务。然而，在资源受限的环境中 `gpsd` 存在一些问题，最主要由于 `gpsd` 被设计为系统启动时运行，系统关闭时停止（或在 USB/蓝牙设备热插/拔出时）。在这种情况下，如果客户端在 `gpsd` 运行之前启动（例如，在连接蓝牙设备之前启动了 GPS 插件），它获取 `gpsd` 信息的唯一方法就是尝试连接到 socket 并频繁尝试，直到成功。

这使得客户端程序非常忙碌，必须不断唤醒检查是否可以连接。在电池供电的系统中，拥有无法频繁睡眠的进程是一件糟糕的事情。此外，`gpsd` 提供的信息粒度也存在问题，因为运行的客户端会收到所有通知，即使它们并不感兴趣。它在每接收到 NMEA 句子时都会发布新的定位，对于大多数 GPS 设备来说，这大约是每五秒一次，每次即使客户端不关心已更改的数据，它们都会被唤醒。

`gpsd` 无法让客户端表示它们只对位置数据感兴趣，或者设备是否有定位感兴趣。即使 GPS 单元是静止的，卫星数据也会不断变化，客户端会在每条消息时被唤醒。由于这些问题，Alan Holmes 手写了 `gypsy`。这是一个 GPS 复用守护进程，提供了对 GPS 信息更精细的控制，并允许程序调用以下对象：

- `Gypsy Position` — 用于位置信息
- `Gypsy Course` — 用于航向信息
- `Gypsy Accuracy` — 用于精度信息

## 实现

首先，安装 Django：

```bash
sudo apt-get install python-django
```

在主目录下创建一个名为 "Web" 的目录，并进入：

```bash
mkdir Web
cd Web
```

接下来，创建一个目录：

```bash
mkdir django_projects
```

进入项目目录并使用 Django 命令行工具启动项目。这将创建基础目录结构和必要的配置文件：

```bash
cd django_projects
django-admin startproject locate
```

> 不要使用 upache、postgresql 或 mysql。这些对于嵌入式设备并不适用。应用将使用 Cherry Py WSGI 服务器和 SQLite。

编辑 `settings.py` 使其如下：

```python
DATABASE_ENGINE = 'sqlite3'
DATABASE_NAME = os.path.join(os.path.dirname(__file__), 'data', 'locate.db')
DATABASE_USER = '' # SQLite3 不使用
DATABASE_PASSWORD = '' # SQLite3 不使用
```

`DATABASE_NAME` 的技巧允许 SQLite 文件系统数据库存储在项目内部的 `data` 文件夹中。在使用版本控制系统时，这是一个优势。类似的技巧适用于站点媒体——在项目根目录创建一个 media 文件夹，然后在 `settings.py` 中编写：

```python
import os, sys
path = os.path.dirname(sys.argv[0])
full_path = os.path.abspath(os.path.join(path, '../media'))
```

然后将 `STATIC_ROOT` 变量设置为该路径：

```python
STATIC_ROOT = full_path
```

最后，在 `urls/media.py` 中导入 Django 设置。将 `static.serve` 设置为：

```python
r'media/(?P<path>.*)$', 'django.views.static.serve',
{'document_root': settings.STATIC_ROOT, 'show_indexes': True},
```

同时在项目目录创建一个名为 "server" 的文件夹。在这个文件夹内部保留一个独立服务器的副本：

```bash
wget http://svn.cherrypy.org/trunk/cherrypy/wsiserver/__init__.py -O wsiserver.py
```

创建一个名为 `run.py` 文件，内容如下：

```python
import wsiserver
# 这可以来自 cherrypy
import os
from django.conf import settings
from django.core.wsgi import get_wsgi_application

if __name__ == "__main__":
    server = wsiserver.pyWSGIServer('0.0.0.0', 8000)
    server.start(get_wsgi_application())
```

## 第 6 章：应用选择

GPS 状态显示如图 6-8 所示，同时附有一个从地图 API 获取的位置小地图。

![](img/001c747b841ab338ed35c50dbdd0c933_178_0.png)

图 6-8

### D-Bus 和 HTTP 请求

可以在不启动某种循环（例如对 `DBusMainLoop` 的调用）的情况下对 D-Bus 查询。

你可以在 `status.py` 中看到它。这种循环条件在本地运行的 Web 应用中不会发生，因此需要一些备选解决方案。

XML-RPC 是一种允许运行在不同操作系统和不同环境下的软件通过互联网进行过程调用的方法。它的远程过程调用使用传输层并以 XML 作为编码。Django 已经提供了一个现成的 XML-RPC 服务器，因此你可以在应用程序内部的 http://code.google.com/p/django_xmlrpc/ 处找到相关代码。我们在 `settings.py` 中定义了一个方法：

```python
XMLRPC_METHODS = {
    # 列出要以表单形式 (name, function) 暴露的方法
    ('django.xmlrpc.views.handle_xmlrpc', 'handle_xmlrpc'),
    ('django.xmlrpc.views.handle_gypsy', 'handle_gypsy'),
}
```

在 `django.xmlrpc.py` 中，创建一个如下的方法签名：

```python
xmlrpc_func(returns='string', args=['string', 'int', 'int', 'int'])
def handle_gypsy(timestamp, latitude, longitude, altitude):
    """从 gypsy XML 对象中获取我们需要的值并将其存储在数据库（或文件系统）中"""
    data = Raw(timestamp=timestamp, lat=latitude, long=longitude, alt=altitude)
    data.save()
    # 返回传入的值（用于调试）
    return "The timestamp is %s, the latitude is %i, the longitude is %i, and the altitude is %i." % (timestamp, latitude, longitude, altitude)
```

XML-RPC 客户端需要将 GPS 对象传递给图 6-9 中 Django 管理对话框所示的 `handle_gypsy` 函数。

![](img/001c747b841ab338ed35c50dbdd0c933_179_0.png)

同样使用 `django_xmlrpc` 集成创建一个 `models.py` 文件来存储从 `django.import` 的 GPS 数据：

```python
class Raw(models.Model):
    time = models.CharField(max_length=200)
    lat = models.FloatField()
    long = models.FloatField()
    alt = models.FloatField()

def __unicode__(self):
    return self.time
```

在 `gypsy.py` 中添加以下内容：

```python
import xmlrpcclient
```

接下来，添加以下内容：

```python
gps.Start():
server = xmlrpcclient.ServerProxy('http://127.0.0.1:8000/xmlrpc/')

def position_changed(fields, timestamp, latitude, longitude, altitude):
    server.handle_gypsy(timestamp, latitude, longitude, altitude)
```

代码将 GPS 数据解析到 Django 应用中。

剩下的就是查询数据库获取最后一个 GPS 位置，以便在 Web 界面中使用。创建一个名为 `geoveapp` 的应用，其 `views.py` 文件如下：

```python
# 在此处创建你的视图。
from django.http import HttpResponse
from locate.django_xmlrpc.models import Raw
from django.shortcuts import render_to_response

def get_position(request):
    latest_GPS = Raw.objects.all().order_by('-id')[:1]
    return render_to_response('location_list.html', {'latest_GPS': latest_GPS})
```

接下来，创建一个模板：

```html
```
