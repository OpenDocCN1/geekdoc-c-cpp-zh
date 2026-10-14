

这里内容很多，所以在深入代码之前请先花时间重读规范。然后一步一步地处理每一部分。准备好继续前进后再返回这里。

第一步，和往常一样，是类型签名：

```
staticFiles :: Request -> ResponseM
```

我们只关心 Request 的路径部分：

```
staticFiles :: Request -> ResponseM
staticFiles { path } =
  ???
```

由于 path 是一个数组，我们需要把路径组合起来形成 fileName：

```
import Data.Array (last, tail, null) ①
import Data.Foldable (class Foldable, foldl, intercalate) ②

staticFiles :: Request -> ResponseM
staticFiles { path } =
  let fileName =
    if null path then "index.html" ③
    else intercalate "/" path in ④
  ???
```

+   ① 将 null 添加到导入列表中。
+   ② 将 intercalate 添加到导入列表中。
+   ③ 处理默认情况。
+   ④ 将路径段组合以生成文件路径。注意，如果你在 Windows 上并且 Node 没有按预期规范化路径分隔符，你将不得不把 / 改为 \\。

接下来，我们将查找 MIME 类型：

```
import Data.Maybe (Maybe(..), maybe) ①

staticFiles :: Request -> ResponseM
staticFiles { path } =
    let fileName =
        if null path then "index.html"
        else intercalate "/" path in
mimeType fileName # maybe HTTPure.forbidden \mime -> do
    ???
```

① 将 maybe 添加到导入列表中。

② 使用我们的 mimeType 函数查找 fileName 的 MIME 类型。如果未找到，我们将响应 forbidden 或 403。否则 Lambda 会被调用并传入 MIME 类型 mime。

现在，我们准备读取整个文件：

```
import Control.Monad.Error.Class (try) ①
import Node.Encoding (Encoding(..))
import Node.FS.Aff (readTextFile)

staticFiles :: Request -> ResponseM
staticFiles { path } =
    let fileName =
        if null path then "index.html"
        else intercalate "/" path in
mimeType fileName # maybe HTTPure.forbidden \mime -> do
    fileData' <- try $ readTextFile ASCII $ staticRoot <> "/" <> fileName ②
    ???
```

① 添加这些导入。

② 使用在 fileName 前加上 staticRoot 的方式读取文件。使用 try 以便我们能正确处理异常。与任何文件路径一样，在 Windows 上也有同样的注意事项。

现在我们处理错误情况：

```
import Data.Either (Either(..), hush, either) ①

staticFiles :: Request -> ResponseM
staticFiles { path } =
    let fileName =
        if null path then "index.html"
        else intercalate "/" path in
    mimeType fileName # maybe HTTPure.forbidden \mime -> do
        fileData' <- try $ readTextFile ASCII $ staticRoot <> "/" <> fileName
        fileData' # either (const HTTPure.notFound) \fileData -> ②
            ???
```

① 将 either 添加到导入列表。

② 如果我们得到 Left 则返回 notFound，即 404 错误。否则，我们用 fileData 调用 Lambda。

现在，我们需要响应 Content-Type 和 Content-Length。所以，我们先构建头部：

```
import Data.String (length) ①
import Data.Newtype (unwrap)

staticFiles :: Request -> ResponseM
staticFiles { path } =
    let fileName =
        if null path then "index.html"
        else intercalate "/" path in
    mimeType fileName # maybe HTTPure.forbidden \mime -> do
        fileData' <- try $ readTextFile ASCII $ staticRoot <> "/" <> fileName
        fileData' # either (const HTTPure.notFound) \fileData ->
            let headers = HTTPure.headers
                [ Tuple "Content-Length" (show $ length fileData) ②
                , Tuple "Content-Type" $ unwrap mime ③
                ] in
            ???
```

① 添加这些导入。

② 根据 fileData 的长度设置 Content-Length。

③ 解包 MediaType 以获取其底层字符串。我们可以使用 unwrap，因为 MediaType 有 Newtype 实例。

现在我们可以用 Primed 版本的 ok 来响应：

```
```haskell
staticFiles :: Request -> ResponseM
staticFiles { path } =
  let fileName =
        if null path then "index.html"
        else intercalate "/" path in
  mimeType fileName # maybe HTTPure.forbidden \mime -> do
    fileData <- try $ readTextFile ASCII $ staticRoot <> "/" <> fileName
    fileData # either (const HTTPure.notFound) \fileData ->
      let headers = HTTPure.headers
            [ Tuple "Content-Length" (show $ length fileData)
            , Tuple "Content-Type" $ unwrap mime
            ] in
      HTTPure.ok' headers fileData
```
```

❶ `Ok'` 接受我们的 `headers`，而 `ok` 则不接受。

最后我们需要调用这个函数。所以去修改 `router` 以处理 HTTP `GET` 并调用 `staticFiles`。然后返回这里。

这是代码更改：

```
```haskell
router :: HandlerEnv -> Request -> ResponseM
router env req@{ body, method } 
  | method == HTTPure.Post =
      let handlers = apiHandlers <#> (_ $ body) in
      case hush $ oneOf handlers of
        Nothing -> HTTPure.badRequest body
        Just reader -> runReaderT reader env
  | method == HTTPure.Get = staticFiles req
  | otherwise = HTTPure.methodNotAllowed
```
```

❶ 将完整的 `Request` 别名为 `req`。

❷ 添加了这个 Guard。

现在，我们准备运行服务器并测试它：

```
```shell
npx spago run
```
```

现在，打开 Postman 并创建一个新的 Tab，输入 URL `localhost:3000`，将方法保持为 `GET`，点击发送时查看是否返回了 `index.html`。

点击响应区域中的 Headers 选项卡并检查 `Content-Type` 和 `Content-Length` 是否

正确设置：

![](img/8c0e9b687c62642e828ccb5481e11313_1755_0.png)

现在将 URL 改为 localhost:3000/index.js 并点击发送：

![](img/8c0e9b687c62642e828ccb5481e11313_1755_1.png)

现在在 URL 中把 .js 改为 .pdf，点击发送，你应该会得到：

![](img/8c0e9b687c62642e828ccb5481e11313_1755_2.png)

看起来我们的静态文件服务器正在工作。

现在，打开浏览器并输入 URL localhost:3000。这应该会显示登录屏幕，就像我们访问 8000 端口时一样。

一旦显示出来，你可以尝试登录看看会发生什么。

当我尝试时，什么也没发生。检查控制台是否有任何错误，除了我们不支持 favicon.ico 之外。

我看到的是：

![](img/8c0e9b687c62642e828ccb5481e11313_1755_3.png)

点击堆栈跟踪顶部显示的 index.js:8236 或其他链接。这应该会带你到类似以下内容：

```
8233  var validateUUID = null;
8234  exports.validateV4UUID = function (str) {
8235    if (validateUUID === null) {
8236      var uuid = require('uuid');
8237      validateUUID = uuid.validate;
8238    }
8239    return validateUUID(str);
8240  };
```

这是在尝试 require UUID Node 模块。但我们运行在浏览器中而不是 Node 中。我们将不得不使用 Parcel 或 Webpack 将我们的 index.js 转换为可在浏览器中运行的东西。

这些打包器会将我们的所有代码以及通过 require 需要的所有 Node 模块代码打包到单个 Javascript 文件中。

我们将为本项目使用 Parcel，因为它很简单。但对于生产服务器，我会使用 Webpack，因为它更可配置。

返回你的客户端项目。

第一步是为客户端项目安装 Parcel：

```
npm install --save-dev parcel@1.12.3 ①
```

① --save-dev 会将此安装保存到 package.json 中的 devDependencies 下。它们仅用于开发的依赖项。

现在，修改你的 Makefile 以匹配：

```
build:
    npx spago bundle-app
    rm -f dist/*.js dist/*.map
    exec npx --node-arg=--max-old-space-size=4096 parcel build index.html ①
    # for Node 15+
    # NODE_OPTIONS='--max-old-space-size=4096' exec npx parcel build --no-minify index.html
```

① 当程序变大时，Parcel 需要更多堆内存，因此 4096 值。我们可能不会遇到这个问题，但我们还是把它放在这里以防万一。

注意我们不再需要创建 dist 文件夹也不需要复制任何文件到那里。Parcel 会为我们完成所有这些。

不过，我们需要忽略 Parcel 为加快构建速度而创建的 .cache 目录。所以，在 .gitignore 中添加以下行：

```
.cache
```

