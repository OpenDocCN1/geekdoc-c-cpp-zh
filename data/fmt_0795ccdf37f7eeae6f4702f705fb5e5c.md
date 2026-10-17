
# 第 10 章：获取和管理软件

## 删除 1 个包

已安装大小：14 M 是否确认 [y/N]: y

注意在安装 `emacs` 时是如何安装了六个包的，而使用 `erase` 子命令只删除了 `emacs` 包本身。虽然 `emacs` 要求安装 `emacs-common`，但 `emacs-common` 并不依赖于 `emacs`，因此它可以留存在系统中而不会破坏依赖关系。运行 `remove emacs-common` 将同时删除这两个包。

删除已安装的一组包的另一种方法是使用 `history` 子命令。通过 `history`，你可以看到你的 `yum` 活动记录和整个事务。换句话说，你安装的所有包都可以使用 `history` 子命令的选项进行卸载。例如：

```
# yum history
ID | 登录用户 | 日期和时间 | 操作 | 更改数量
96 | Chris Ne <cnegus> | 2016-12-10 06:25 | Install | 2

# yum history info 96
事务 ID : 96
命令行 : install emacs

# yum undo 96
正在撤销事务 96，时间为 2014年12月14日 06:25:20
Dep-Install emacs-common-1:24.4-3-fc21.x86_64 @updates
Dep-Install libXaw-1.0.12-4-fc21.x86_64 @fedora
```

在撤销事务后，你可以查看事务以确切知道涉及哪些包。查看事务可以防止你误删想要保留的包。通过撤销事务 96，你可以移除在该事务期间安装的所有包。如果你正尝试撤销一个包含数十个或数百个包的安装，`undo` 是一个非常实用的选项。

## 更新软件包

当软件包的新版本发布时，它们有时会位于单独的更新存储库中，或者直接被添加到原始存储库中。如果一个包有多个可用版本（无论是在同一个存储库还是另一个启用的存储库中），`yum` 在你安装包时会提供最新版本。如果之后出现了新版本，你可以使用 `update` 命令下载并安装该包的新版本。

`check-update` 命令可以检查更新。`update` 命令可更新单个包，也可用于更新所有已安装且有更新的包。或者你也可以简单地更新单个包（例如 `cups` 包）。例如：

```
# yum check-update
kernel.x86_64 3.10.0-126.3.el7 rhel-7-server-rpms
```

![](img/3886a4c1a684ab63e25e82e0a2d63de9_288_0.png)

kernel-headers.x86_64 3.10.0-126.3.el17 rhel-7-server-rpms

```
# yum check-update
kernel.x86_64 3.10.0-126.3.el7 rhel-7-server-rpms

kernel-headers.x86_64 3.10.0-126.3.el17 rhel-7-server-rpms
```

### yum update

```
# yum update
正在解析依赖
--> kernel.x86_64 3.10.0-126.3.el7 rhel-7-server-rpms
--> kernel-headers.x86_64 3.10.0-126.3.el17 rhel-7-server-rpms
最后将更新依赖
--> kernel.x86_64 3.10.0-126.3.el7 rhel-7-server-rpms
--> kernel-headers.x86_64 3.10.0-126.3.el17 rhel-7-server-rpms
```

事务摘要
===================
升级 2 个包 (+0 相关依赖包)
总下载大小：0 M
是否确认 [y/N]: y

## 清理缓存

`clean` 命令可以清理 `yum` 缓存。你可以使用它来删除所有已下载的包和元数据，这在磁盘空间紧张时非常有用。

### 清理元数据

`clean` 命令可以清理 `yum` 缓存。你可以使用它来删除所有已下载的包和元数据，这在磁盘空间紧张时非常有用。例如：

```bash
# yum clean metadata
```

### 清理包

`clean` 命令可以清理 `yum` 缓存。你可以使用它来删除所有已下载的包和元数据，这在磁盘空间紧张时非常有用。例如：

```bash
# yum clean packages
```

### 清理头部

`clean` 命令可以清理 `yum` 缓存。你可以使用它来删除所有已下载的包和元数据，这在磁盘空间紧张时非常有用。例如：

```bash
# yum clean headers
```

### 清理数据库

`clean` 命令可以清理 `yum` 缓存。你可以使用它来删除所有已下载的包和元数据，这在磁盘空间紧张时非常有用。例如：

```bash
# yum clean db
```

### 清理过期

`clean` 命令可以清理 `yum` 缓存。你可以使用它来删除所有已下载的包和元数据，这在磁盘空间紧张时非常有用。例如：

```bash
# yum clean expire
```

### 清理所有

`clean` 命令可以清理 `yum` 缓存。你可以使用它来删除所有已下载的包和元数据，这在磁盘空间紧张时非常有用。例如：

```bash
# yum clean all
```
