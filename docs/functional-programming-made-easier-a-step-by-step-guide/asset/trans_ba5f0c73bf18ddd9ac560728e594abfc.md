

② 当浏览器发送 OPTIONS 时，我们将响应以允许来自任何来源的所有方法和标头。

③ 使用 emptyResponse 返回空主体进行响应，因为 OPTIONS 只需要返回标头。

但，我们不会做任何这些。我只是把它放在这里供将来参考，即如果你发现自己处于需要在服务器上支持 CORS 的情况。

## 30.9.2. 静态文件服务器解决方案

与其处理 CORS，我们将让我们的服务器为浏览器提供 index.html 和其他文件，而不是依赖 Python 的 SimpleHTTPServer。

这意味着文件和 API 调用将来自完全相同的服务器，从而完全避免 CORS 问题。

要做到这一点，我们将不得不支持 GET 方法，因为浏览器就是用它从 Web 服务器检索文件的。

但，我们也希望确保不会提供任何文件。因此，我们将支持可接受文件类型的白名单，即可以安全提供的文件扩展名。

我们要做的另一件事是在构建客户端时将可以提供的文件隔离起来。这些文件将由我们的服务器提供。

首先，让我们更改构建以将适当的文件复制到 dist，即分发文件夹。为此，我们需要在客户端修改 Makefile：

```
build:
    npx spago bundle-app ①
    mkdir -p dist ②
    cp {index.html,index.js} dist ③

.PHONY: build ④
```

① 将 build 改为 bundle-app。bundle-app 是 spago 中的构建选项，用于将你的所有代码构建成单个 index.js 文件供浏览器使用。

② -p 选项如果目录已存在则不会报错。

③ 将 index.html 和 index.js 都复制到 dist。确保文件列表中没有空格。

④ 从文件中删除了 run 目标并从这一行中删除。

对客户端的 Makefile 进行上述更改。

接下来，将 index.js 添加到你的 .gitignore 中：

```
/bower_components/
/node_modules/
/.pulp-cache/
/output/
/generated-docs/
/.psc-package/
/.psc*
/.purs*
/.psa*
/.spago
index.js ①
```

① 这是 bundle-app 命令的输出。

现在运行以创建分发版本，即发布版本：

```
make build
```

你现在应该会看到一个包含适当文件的 dist 文件夹。

请记住，每次我们更改客户端时，我们都必须运行 make build 来构建并复制文件，以便我们的服务器可以将更新后的文件提供给浏览器。

接下来，将以下行添加到 spago init 创建的 .gitignore 文件中：

```
dist
```

这将从 git 仓库中排除此目录。

如果你在 VSCode 中编码，你应该会注意到 index.js 和 dist 目录是灰色的。

现在，切换到你的服务器项目。

我们将支持提供文件，但在这样做之前让我们先制定一个计划：

- 维护一个允许检索的文件扩展名白名单
- 根据文件扩展名返回适当的 MIME 类型
- 从 ../client/dist 读取文件，该路径相对于服务器目录

首先，我们将在 Main.purs 中创建一个白名单：

```
whitelistExtensions :: Array String
whitelistExtensions = [ "js", "html", "jpg", "png" ]
```

现在将此添加到服务器项目的 Main 中。

如果我们需要不同文件类型，可以将此列表添加到其中。这只是额外的预防措施，以防我们不小心将不同扩展名的文件放入 client/dist 文件夹。至少我们的服务器不会提供它。

接下来，我们将编写一个函数，它接受文件扩展名并返回适当的 MIME 类型。MIME 类型将告诉我们要在响应中的 Content-Type HTTP 标头中放置什么。此信息将告诉浏览器如何处理文件。

首先，创建文件扩展名及其对应 MIME 类型的映射。使用 Data.MediaType 和 Data.MediaType.Common 来帮助你。将其命名为 mimeTypes。准备好继续时返回此处。

首先，我们需要在 spago.dhall 文件中添加 media-types，以便我们可以使用此库：

```
npx spago install media-types
```

然后构建：

```
npx spago build
```

然后我们可以将以下代码添加到 Main：

```
import Data.Map (Map) ①
import Data.Map as Map
import Data.MediaType (MediaType)
import Data.MediaType.Common as MIME
import Data.Tuple (Tuple(..))

mimeTypes :: Map String MediaType
mimeTypes = Map.fromFoldable [ ②
    Tuple "js" MIME.applicationJavascript ③
  , Tuple "html" MIME.textHTML
  , Tuple "jpg" MIME.imageJPEG
  , Tuple "png" MIME.imagePNG
]
```

① 添加了这些导入。

② 使用 Map 中的 fromFoldable 从键值元组的数组创建我们的 Map。

③ 数组中的每个条目都是一个元组，其中第一个位置是键，第二个是值。

现在，我看着这个，似乎我们有两个真实来源。whitelistExtensions 和 mimeTypes。想象一下向 mimeTypes 添加内容但忘记添加到 whitelistExtensions，或者反之亦然。

删除 whitelistExtensions，我们将使用 mimeTypes 作为白名单。当我们找不到 MIME 类型时，我们将把该文件视为被列入黑名单。

接下来，添加一个名为 mimeType 的函数，它接受 fileName 并返回其 MIME 类型。使用 mimeTypes 来查找其类型。完成后返回此处继续阅读。

首先，我们从类型签名开始：

```
mimeType :: String -> Maybe MediaType ①
```

① 返回一个 Maybe，因为我们可能找不到 MIME 类型。在这种情况下，我们将此文件请求视为无效，因为它不在我们的白名单中。

接下来，我们将实现开始部分：

```
mimeType :: String -> Maybe MediaType
mimeType fileName = do ①
  ???
```

① 在 Maybe Monad 中编码。

下一步是获取文件扩展名：

```
import Data.Array (last, tail) ①
import Data.String.Common (split)
import Data.String.Pattern (Pattern(..))

mimeType :: String -> Maybe MediaType
mimeType fileName = do
  ext <- last ==< (tail $ split (Pattern ".") fileName) ② ③
  ???
```

① 添加了这些导入。

② 按 . 分割 fileName 并丢弃头部，即文件扩展名之前的部分，然后获取数组中的最后一项。

③ 在 Maybe Monad 中，我们可以提取 Just 结果或短路返回 Nothing 给调用者。

最后，我们将在 mimeTypes Map 中查找文件扩展名：

```
import Data.String.Common (split, toLower) ①

mimeType :: String -> Maybe MediaType
mimeType fileName = do
  ext <- last ==< (tail $ split (Pattern ".") fileName)
  Map.lookup (toLower ext) mimeTypes ②
```

① 添加了 toLower 到输入列表。

② Map.lookup 将返回一个 Maybe。

由于我们有一个只有 2 行代码的 do 块，我们可以将其重写为：

```
mimeType :: String -> Maybe MediaType
mimeType fileName = (last ==< (tail $ split (Pattern ".") fileName)) >>=
  flip Map.lookup mimeTypes <<< toLower
```

我不确定我更喜欢这个版本。你可以自己选择。我将保留 do 块版本。

现在，将以下内容添加到你的代码中：

```
staticRoot :: String
staticRoot = "../client/dist"
```

这是所有静态文件请求的基础目录。这些文件被认为是静态的，因为它们不是由我们的服务器动态生成的文件，即它不是服务器渲染的内容，如 JSP、ASP.NET、WebForms、Next.js 等技术中可能找到的那样，或在服务器上运行 React 或 Angular 时。

接下来，编写一个名为 staticFiles 的函数，它将接受一个 Request 并返回一个 ResponseM。从该请求中，它将使用 path，即一个数组，并与 staticRoot 组合构建到文件的路径。如果路径为空，则 index.html 将为默认值。

然后，如果且仅当它在白名单中，即我们可以为其文件扩展名找到 MIME 类型时，该文件将被读取并其内容返回给客户端。

请参阅我们在服务器的账户管理器中如何执行 readTextFile 作为参考，但在这种情况下，使用 Control.Monad.Error.Class 中的 try，并且当你无法读取文件时发送 HTTPure.notFound，即 404。

最后，你将希望在 HTTP 标头中发送 Content-Length 和 Content-Type。这可以通过 HTTPure.headers 实现，并使用 ok 的 Primed 版本，即 HTTPure.ok'。

