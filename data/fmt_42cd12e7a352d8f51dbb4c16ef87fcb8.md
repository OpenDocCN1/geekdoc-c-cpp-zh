
```
$ mkdir /path/to/your/repository/ubuntu
$ mkdir /path/to/your/repository/ubuntu/conf
$ mkdir /path/to/your/repository/ubuntu/incoming
```

这是 `repropro` 配置文件。你的 distributions 文件应该像这样：

```
Codename: karmic
Suite: karmic
Components: main
Architectures: i386 source
Description: Repo for book
```

此文件应该放在 `/path/to/your/repository/ubuntu/conf`。

## 向仓库添加包

要向仓库添加包，请使用以下命令：

```
$ repropro -b include jaunty name_of_file.changes
```

也可以通过以下操作添加包：

```
$ repropro -b include-udeb karmic some-package.deb
```

在处理旧版本发行版（例如 hardy）时，你可能会发现来自较新发行版（例如 intrepid）的一些应用程序功能有用。在这种情况下，有必要将应用程序“回移植”（backport）到旧发行版。

## 从仓库中移除包

可以使用以下命令移除包：

```
$ repropro -V /path/to/repository/ubuntu remove karmic some-package.deb
```

## 回移植 KVM

在 `sources.list` 中添加 intrepid 的源，如下所示：

```
deb-src http://archive.ubuntu.com/ubuntu/ intrepid main restricted
```

注释掉 `sources.list` 中的其他 deb-src 行。接下来，运行以下命令：

```
$ apt-get source kvm
```

进入解压后的文件夹（在此情况下为 `kvm-72+dfsg`）并运行：

```
$ debuild
```

如果这给出了如下构建依赖：

```
dpkg-checkbuilddeps: Unmet build dependencies: quilt (>= 0.40) uuid-dev libssd1.2-dev libasound2-dev libnutils-dev nasm textizhtml bcc iasl
dpkg-buildpackage: warning: Build dependencies/conflicts unsatisfied; aborting.
```

你需要添加：

```
$ sudo apt-get build-dev kvm
```

然后再次运行 `debuild`。这会在父目录创建 `.deb` 包。

## 第 5 章：软件包打包

## PBuilder

你可以按照我们之前展示的方法来构建包，但你必须已经在运行的系统中安装了你所构建的包的所有构建依赖。

工具 `pbuilder` 可以帮助实现这一点。`pbuilder` 会自动检查构建依赖，因为它是在一个最小化的 Ubuntu 安装中构建包的，并根据 `Debian/control` 文件下载构建依赖。

`pbuilder` 的主要目标与 Debian 中的其他自动构建系统不同，不同之处它并不尝试构建尽可能多的包。它不会尝试猜测一个包需要什么，而且在大多数情况下，如果有可选方案，它会尝试最糟糕的选项。

## 配置 PBuilder

配置 `pbuilder` 是一个好主意。在 `/etc` 目录下有许多方法可以实现这一点，其中 `pbuilder` 的主配置文件名为 `.pbuilderrc`。

编辑此文件使其如下所示：

```
BASEGTZ=/var/cache/pbuilder/base.tgz
#EXTRAPACKAGES=gcc3.0-athlon-builder
#export DEBIAN_BUILDARCH=athlon
BUILDPLACE=/var/cache/pbuilder/
MIRRORPATH=http://archive.ubuntu.com/ubuntu
USEPROC=yes
USEDEVOPTS=yes
USEDEVFS=no
BUILDDIR=/var/cache/pbuilder/result/
## 指定发行版将强制在 "pbuilder update" 中使用该版
DISTRIBUTION=""
## 指定发行版的组件（默认是 "main"）
#COMPONENTS="main restricted universe multiverse"
# 指定 APT 缓存路径
APTCACHE_PATH=/var/cache/pbuilder/aptcache/
APTCACHEHERDLINE="yes"
REEMOVEPACKAGES=""
#HOOKDIR=/usr/lib/pbuilder/hooks/
HOOKDIR=""
# 让 debconf 不与用户交互
export DEBIAN_FRONTEND="noninteractive"
DEBIMAIL=""
## 用于 pbuilder debuild (sudo -E 保持环境不变)
BUILDSOURCEROOTDIR="fakeroot"
BUILDEREROOTID=sudo
# 为了满足构建依赖；默认是一个内部的 shell
# 实现，它的速度较慢；有两种替代
# 实现，即“实验性”实现：
# pbuilder-satisfydepends-experimental，它可能用于从实验性或
# 低 APT 优先级的仓库中提取包；
# "aptitude" 实现，它将使用 aptitude 来解析构建依赖和
# 构建冲突，这有助于处理复杂情况，但它不支持``````

## 支持未签名的 APT 仓库

BUILDERSATISFYDEPENDSCMD="/usr/lib/pbuilder/pbuilder-satisfydepends"

#-传递给 dpkg-buildpackage 的命令行选项。

DEBBUILDOPTS="-IXXX -IXXX"

## APT 配置文件目录

APT_CONF="**"

# pbuilder 在 chroot 内部使用的用户名和 ID。需要 fakeroot， 

BUILDERID=1234

BUILDUSERNAME=pbuilder

# BINDMAPTS 是 chroot 内部要挂载项的空格分隔列表

BINDMAPTS="**"

## 设置为 'build' own debstrap 变体。

DEBOOTSTRAPOTS="[0]- variant=build"

## 或取消设置以使其不是构建类型。

## unset DEBOOTSTRAPOTS

# 设置我在 pbuilder 内部使用的 PATH：默认是 /usr/sbin:/usr/bin:/sbin:/bin:/usr/XLR16/bin

EXPORT PATH=/usr/sbin:/usr/bin:/sbin:/bin:/usr/XLR16/bin"

## SHELL 变量在 pbuilder 内部被 'shell' 命令使用；它们可能需要合理的值

EXPORT SHELL="/bash"

# debstrap 命令的名字。

DEBOOTSTRAP="debstrap"

## pkgname-logfile 的默认文件扩展名

PKGNAME_LOGFILE_EXTENSION="_${dpkg -print-architecture}.build"

## 默认的 PKGNAME_LOGFILE

PKGNAME_LOGFILE="**"

```

这为 `pbuilder` 提供了一些配置默认值。

可以使用 bash 脚本对 `pbuilder` 进行脚本化。以下脚本允许为任何 Ubuntu 发行版创建 Debian 包（名称作为命令行参数传递给 `pbuilder`）。修改 `/home/<user>/.pbuilderrc` 文件使其看起来如下代码所示。此代码仅供参考。请从你的配置中下载此文件。

```

#USE_SYSTEM_DIST=1

#DEFAULT_DIST="hardy"

#OTHERMIRROR="http://localhost:8000/test/ http://localhost:8000/extra/hardy_main/"

UBUNTU_UPDATES=1

UBUNTU_SECURITY=1

UBUNTU_BACKPORTS=1

UBUNTU_PROPOSED=0

DEBIAN_SECURITY=1

DEBIANLIST="jaunty testing unstable experimental lenny"

DEBIANLIST="stable testing unstable experimental lenny"

UBUNTU_MIRROR="http://archive.ubuntu.com/ubuntu/"

DEBIAN_MIRROR="http://ftp.debian.org/debian/"

if [ -z "${DIST}" ]; then

``````
if [ -n "${DEFAULT_DIST}" ]; then
  DIST="${DEFAULT_DIST}"
elif [ "${SYSTEM_DIST}" ]; then
  DIST=$(lsb_release --short)
else
  if [ -r "debian/changelog" ]; then
    DIST=$(dpkg-parsechangelog | awk '/Distribution:/ {print $2}')
    # 使用 unstable 组处理 debian 实验性包。
    if [ "${DIST}" = "debian experimental" ]; then
      DIST="unstable"
    fi
  fi
fi

``````

echo "${DEBIANLIST}" | grep -q "${DIST}" || {

  echo "Distribution ${DIST} is not in ${DEBIANLIST}"

  exit 1

}

MIRROR="${UBUNTU_MIRROR}"

# 

if [ -z "${DIST}" ]; then

  DIST="hardy"

fi

if [ -z "${MIRROR}" ]; then

  MIRROR="${DEBIAN_MIRROR}"

fi

echo "Building ${DIST} using ${MIRROR}..."

# 示例构建命令

## pbuilder build -d ${DIST}

```

## 配置 Actions

钩脚本（Hook scripts）用于你希望在 `pbuilder` 运行期间特定时刻执行某些操作。这些操作也可以是脚本。

钩子目录可以通过变量 `HOOKDIR` 定义。可以在命令行中这样设置：

```bash
$ sudo HOOKDIR=/path/to/hookdir pbuilder -build file.dsc
```

你也可以按照以下方式设置：

```bash
$ pbuilder -hookdir /path/to/hookdir -build whatever-else-you-want
```

钩脚本的名称必须采用 `X<digit><digit><whatever-else-you-want>` 的形式，类似于启动脚本。这里是一个 `c0shell hook<whatever-else-you-want>` 钩脚本示例，它会在构建失败时调用 shell。

```bash
#!/bin/bash

## invoke shell if build fails.

apt-get install -y - force-yes vim less

cd /tmp/pbbuild/debian/

/bin/bash <dev/tty > /dev/tty 2 /dev/tty
```

# 使用 PBbuilder 进行额外的钩子操作

我们发现的一些非常有用的钩子操作命令如下。它们以第一个字母 A 开头。

```bash
A<digit><digit><whatever-else-you-want
```

这在构建开始之前执行——解压构建系统、解压源码，并满足构建依赖。

B 的用法如下：

```bash
B<digit><digit><whatever-else-you-want
```

这在构建系统成功完成构建之后、在拷贝回构建结果之前执行。

C 的用法如下：

```bash
C<digit><digit><whatever-else-you-want
```

这在构建失败之后、清理之前执行。

D 的用法如下：

```bash
D<digit><digit><whatever-else-you-want
```

## 第 5 章：应用程序打包

这在 chroot 内部解压源码之前以及在设置 chroot 环境之后执行。

## 钩脚本资源

在安装 Bazaar 后（`sudo apt-get install bzr`），检查以下内容：

```bash
bzr branch lp:ubuntu-members/pbbuilder/pbbuilder-hooks
```

这包含了一些示例脚本。包括 `D01aptdate` 的使用，它在继续后续之前运行 `apt-get update`，以及列出缺失文件的 `B01list-missing`。

# 挂载包仓库供 Builder 使用

绑定挂载（Bind mounting）目录对许多任务都有用。最有用的功能之一是挂载一个包仓库目录：

```bash
BINDMOUNTS=/var/cache/pbbuilder/result

# cat /var/cache/pbbuilder/hooks/D07results

#/bin/sh

cd /var/cache/pbbuilder/result/

/usr/bin/dpkg-scanpackages . /dev/null /var/cache/pbbuilder/result/Packages

/usr/bin/apt-get updates
```

通过这种方式，你可以在 `OTHERREPOSITORY` 变量中使用 `/var/cache/pbbuilder/result`。

# Ubuntu 策略

位于 http://people.canonical.com/-cjwatson/ubuntu-policy/policy 的 Ubuntu 策略文档描述了“Ubuntu发行版的策略要求”。它还讨论了与包相关的策略，例如每个包包含在Ubuntu发行版中必须满足的技术要求。它紧参考了 Debian 策略。

这份文档极其重要。请阅读它。需要了解的一点是 Ubuntu 软件包存档是如何划分类别的：

# 类别

类别分为受限（restricted）、宇宙（universe）和多宇宙（multiverse），每个类别对于包包含在其中有不同的要求。

- **Main（主仓库）**——main 中的软件包在编译或执行时不需要 main 之外的软件包（因此，该包不能对非 main 软件包声明“Depends”、“Recommends”或“Build-Depends” 依赖关系）。
- **Restricted（受限）**——restricted 中的软件包可能无法提供源代码，并且可能不允许进行修改。
- **Universe（宇宙）**——此类别中的软件包不受 Ubuntu 开发者或 Canonical 支持。此外，软件包在编译或执行时不需要 main 和 universe 之外的软件包（因此，该包不能对非 main 且非 universe 的软件包声明“Depends”、“Recommends”或“Build-Depends” 依赖关系）。
- **Multiverse（多宇宙）**——如果源码不可用、不允许修改，或者受到专利或其他法律问题的限制导致其分发出现问题，则软件包必须放在 multiverse 中。

每个包必须在 `/usr/share/doc/package/copyright` 下提供版权文件和分发许可。

# 章节（Sections）

上述类别进一步细分为章节。这些章节在 Debian 软件包的控制文件中指定。它们对于将软件包组织成逻辑块非常有用。可选章节包括 admin、graphics、web、X11 和元软件包（metapackages）。完整列表可在策略文档本身中找到。关于元软件包的使用将在第 11 章“整合一切”中进行介绍。

Ubuntu 存档的维护者可能会覆盖章节值以确保 Ubuntu 发行版致性。因此，在包中包含此信息很重要。

## 总结

本章展示了打包中用到的一些基本工具，并涵盖了如何创建一个包含 Debian 软件包所需文件的简单存档。它向你展示了如何为软件包设置本地仓库。你还看到了如何使用和自定义 `pbuilder` 以及其他自定义脚本，这些脚本可以在 `pbuilder` 运行之前、期间或之后运行。最后，我们讨论了 Ubuntu 策略文档。

# 6 应用程序选择

因此，驱动企业环境采用移动设备的一个因素是安全性。密码保护、远程擦除和物理设备追踪是许多考虑为员工配备移动设备的公司所提到的三个关键因素。Ubuntu 提供了一个创建加密目录的功能。你可以在设备上这样设置：

```bash
$ sudo apt-get install ecryptfs-utils
```

然后运行以下：

```bash
$ ecryptfs-setup-private
```
