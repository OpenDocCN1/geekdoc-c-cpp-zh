
`libvacodec` 末尾的星号用于 `germinate` 代码中的正则匹配，将所有以 `libvacodec` 开头的内容放入该种子的黑名单中。

种子文件中需要注意的其他内容是替换变量。包含替换变量的包将扩展为这些变量的每种可能组合的每一个包。例如：

- Kernel-Stem: linux linux-image

== i386 ==

- `$(Kernel-Stem)-generic-pae` [i386]
- `linux-headers-generic-pae` [i386]
- `$(Kernel-Stem)-virtual` [i386]
- `linux-headers-virtual` [i386]

种子条目后面也可以跟随方括号。`[powerpc]` 表示 `language-support-$` 包不应在 powerpc 架构上使用。反之亦然，后面跟着 `[lpia 1386]`（不带感叹号）的种子条目表示它们应该只在 LPIA 和 i386 架构上使用。

最后，如果种子中的包名以 `%` 开头，则将展开为来自给定源包的所有二进制文件。

## 萌发种子

如前所述，原始种子文件通过 `germinate` 程序被萌发为完整的包列表。`germinate` 程序需要存在某些默认种子文件才能工作。这些种子文件中最重要的（强制性的）是 `STRUCTURE`、`supported` 和 `blacklist`。

这些强制性文件不一定包含任何内容，但为了让 `germinate` 工作必须存在。

`STRUCTURE` 是一个特殊文件，列出了种子以及它们相互依赖的关系。karmic netbook 的 `STRUCTURE` 文件如下：

- platform.karmic
- netbook-remix: desktop-common
- live: netbook-remix
- ship-live: live
- supported: netbook-remix ship-live supported-common

种子文件的名称后面跟着一个冒号。冒号后的行内空格表示依赖关系。通过查看 `germinate` 输出中的 dot 文件，可以图形化地看到种子之间的关系。图 11-2 显示了 Ubuntu Netbook Remix 的图形化 `germinate` 输出，可以在 `http://people .ubuntu.com/~ubuntu-archive/germinate-output/unr.karmic/structure.dot` 获取。

![](img/001c747b841ab338ed35c50dbdd0c933_268_0.png)

图 11-2 structure 文件列出了种子之间的继承关系。它是一个如下所示的有序序列：

```
SEED: [INHERITED]
```

`INHERITED` 是用空格分隔的种子列表。例如，`netbook-remix: desktop-common` 在之前的 `STRUCTURE` 文件中 `netbook-remix` 种子依赖于 `desktop-common` 种子。任何如下所示的行：

```
include BRANCH
```

位于下方会导致另一个种子被包含。`supported` 种子列出了所有构建发行版所需的包（但出于空间考虑不一定包含在最终镜像中），因此，它不会将种子构建依赖项的所有依赖项添加到输出中，除非它们在种子列表中。与其他任何种子一样，`supported` 种子可能包含其自己的内容。（*此处由于原文存在大量重复段落，已按要求进行翻译并保持格式*）

# 第 11 章：整合一切

```
archive_base/ports: #ports.ubuntu.com/ubuntu-ports/

archive_base/ppa: %(archive_base/ports)s

archive_base/ia64: %(archive_base/ports)s

archive_base/lpia: %(archive_base/ports)s

archive_base/powerpc: %(archive_base/ports)s

archive_base/sparc: %(archive_base/ports)s

archive_base/armel: %(archive_base/ports)s

components: main restricted
```

```
[karmic/bzr]

seed_base: bzr+ssh://bazaar.launchpad.net/#~ubuntu-core-dev/ubuntu-seeds/

seed_dist: unr%(dist)
```

更改后，seed 看起来将如下所示（请阅读注释）：

```
[DEFAULT]

dist: karmic

[Karmic]

seeds: netbook-test

architectures: i386

# 在此处放置你的 seed 文件的路径。该路径下应该包含

# .karmic 和 netbook.karmic。

seed_base: //home/user/devel/path/to/seeds/

# 我们在此处用逗号分隔仓库。第一个仓库是

# 缓存 debian 仓库，第二个是包含修改后包的本地仓库。

archive_base: http://localhost:9999/ubuntu/, file:/home/user/devel/path/to/repos

# 此处将设置包含 seed 文件的目录名称

seed_dist: netbook%(dist)
```

运行更新脚本：

```
$ ./update
```

此脚本调用 `germinate-update-metapackage`，它负责构建元包（metapackage）。

`germinate-update-metapackage` 会重命名当前目录，更新 `debian/control` 以反映 seed 当前的内容，并更新 `debian/changelog` 以描述其所做的更改。现在可以使用 `dpkg` 手动重构该包。

# 构建元包

将 `unr-meta` 目录重命名为新名称。这将是源包的新名称。例如，将 `unr-meta-1.157` 重命名为 `netbook-meta-1.157`。

这是重命名源包，而不是新元包的名称。该名称是在 `debian control` 文件的第二个段（stanza）中定义的。

接下来，进入 `netbook-meta-1.157` 目录然后进入 `debian` 子目录。编辑控制文件并将旧的包名（例如 `ubuntu-netbook-remix`）替换为新的重构包名（例如 `ubuntu-netbook-example`）。一个控制文件的示例如下：

```
Source: netbook-meta

Section: packages

Priority: optional

Maintainer: Ubuntu Mobile Developers <ubuntu-mobile@lists.ubuntu.com>

Standards-Version: 3.7.3

Build-Depends: debhelper (>= 4), germinate (>= 0.42)

Package: ubuntu-netbook-example

Architecture: any

Depends: ${ubuntu-netbook-example:Depends}

Recommends: ${ubuntu-netbook-example:Recommends}

Description: The Ubuntu Netbook Example system

此包依赖于 Ubuntu Netbook Remix 系统中的所有包
```

它也用于帮助确保适当升级，因此建议不要将其删除。

保存此文件并编辑 `debian/rules` 文件。如果你更改了 `STRUCTURE` 文件中“Terminating the Seeds”部分中的主文件名（例如，从 `netbook-remix` 改为 `netbook-example`），你也应该替换它。这里是一个规则文件的示例：

```
#!/usr/bin/make -f

clean

dh_testdir

dh_clean

rm -rf build-stamp *.old bootstrap-dir

DEB_BUILD_ARCH ?=$(shell dpkg-architecture -qDEB_BUILD_ARCH)

build:build-stamp

build-stamp: netbook-example-$(DEB_BUILD_ARCH)

dh_clean

for seed in netbook-example; do \

  package=ubuntu-${seed};\n

  (printf "\${package}:Depends}=*"; perl -pe 's/\n/, /g' '$${seed}-$(DEB_BUILD_ARCH)}\' echo \

>> debian/\${package}.subvars; \

  (printf "\${package}:Recommends}=*"; perl -pe 's/\n/, /g' '$${seed}-$(DEB_BUILD_ARCH)}\' echo \\ \

>> debian/\${package}.subvars; \

done

Done

touch $$

install:build-stamp

binary-arch:install

dh_testdir -a

dh_testroot -a

dh_installdocs -a

dh_installchangelogs -a

dh_compress -a

dh_fixperms -a

dh_instaldeb -a

dh_gencontrol -a

dh_md5sums -a

dh_builddebb -a

binary-indep:

dh_testdir -i

dh_testroot -i

dh_installdocs -i

dh_installchangelogs -i

dh_compress -i

dh_fixperms -i

dh_instaldeb -i

dh_gencontrol -i

dh_md5sums -i

dh_builddebb -i

binary: binary-indep binary-arch

.PHONY: binary-arch binary-arch
```
