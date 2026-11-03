

## 颜色处理函数

```c
int gdImageColorAllocate(gdImagePtr im, int r, int g, int b)
int gdImageColorAllocateAlpha(gdImagePtr im, int r, int g, int b, int a)
int gdImageColorClosest(gdImagePtr im, int r, int g, int b)
int gdImageColorClosestAlpha(gdImagePtr im, int r, int g, int b, int a)
int gdImageColorClosestHWB(gdImagePtr im, int r, int g, int b)
int gdImageColorExact(gdImagePtr im, int r, int g, int b)
int gdImageColorResolve(gdImagePtr im, int r, int g, int b)
int gdImageColorResolveAlpha(gdImagePtr im, int r, int g, int b, int a)
int gdImageColorsTotal(gdImagePtr im)(MACRO)
int gdImageRed(gdImagePtr im, int c)(MACRO)
int gdImageGreen(gdImagePtr im, int c)(MACRO)
int gdImageBlue(gdImagePtr im, int c)(MACRO)
int gdImageGetInterlaced(gdImagePtr im)(MACRO)
int gdImageGetTransparent(gdImagePtr im)(MACRO)
void gdImageColorDeallocate(gdImagePtr im, int color)
void gdImageColorTransparent(gdImagePtr im, int color)
void gdTrueColor(int red, int green, int blue)(MACRO)
void gdTrueColorAlpha(int red, int green, int blue, int alpha)(MACRO)
```

## 图像缩放函数

```c
void gdImageCopy(gdImagePtr dst, gdImagePtr src, int dstX, int dstY, int srcX, int srcY, int w, int h)
void gdImageCopyResized(gdImagePtr dst, gdImagePtr src, int dstX, int dstY, int srcX, int srcY, int destW, int destH, int srcW, int srcH)
void gdImageCopyResampled(gdImagePtr dst, gdImagePtr src, int dstX, int dstY, int srcX, int srcY, int destW, int destH, int srcW, int srcH)
void gdImageCopyRotated(gdImagePtr dst, gdImagePtr src, double dstX, double dstY, int srcX, int srcY, int srcW, int srcH, int angle)
void gdImageCopyMerge(gdImagePtr dst, gdImagePtr src, int dstX, int dstY, int srcX, int srcY, int w, int h, int pct)
void gdImageCopyMergeGray(gdImagePtr dst, gdImagePtr src, int dstX, int dstY, int srcX, int srcY, int w, int h, int pct)
void gdImagePaletteCopy(gdImagePtr dst, gdImagePtr src)
void gdImageSquareToCircle(gdImagePtr im, int radius)
void gdImageSharpen(gdImagePtr im, int pct)
```

## 杂项函数

```c
int gdImageCompare(gdImagePtr im1, gdImagePtr im2)
void gdImageInterlace(gdImagePtr im, int interlace)
void gdFree(void *ptr)
```

要使用这样的库，你需要熟悉这些参数，它们通常是库自身定义的数据类型，例如 `gdImagePtr`，它是一个指向某种结构的指针，该结构包含了待处理或存储图像的所有数据。这些内容起初可能看起来有些陌生，但过一段时间后，你就会开始习惯这种语法和在线文档，并逐渐从这种复杂性中看出规律。

## 7 Apache C 模块

### 7.1 更安全的 C Web 应用程序

在现实生活中，很少有Web管理员会愿意让任何人把C程序作为CGI内容生成器来运行，因为存在崩溃和核心转储的风险。然而，Apache服务器本身就是用C编写的，并且其开发工具附带了一些简单的实用程序，允许你创建代码存根，将你的C程序放入其中，并在它们作为服务器的一部分加载、在一种“沙箱”中安全管理时，以Apache模块的形式运行。这里我们将采用之前的一个示例，将其转化为一个Apache模块。

一个名为 `apxs2` 的实用程序包含在 Apache2 开发库中，可以调用它为一个程序生成代码存根，该程序可编译成模块，由 Apache Web 服务器加载和管理。这些模块可用于执行各种各样的任务，但在我们的例子中，我们将做的事情类似于 IIS 服务器中的 ISAPI DLL。`apxs2` 实用程序的确切位置因你使用的Linux发行版而异，但在OpenSuse中，它的运行方式如下。

在终端中输入：`apxs2 -n labelmaker -g`

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_66_0.png)

这会创建一个你指定名称的文件夹（labelmaker），以及一个 **Makefile**、一个可供 Make 工具使用的 **modules.mk** 文件，还有一个名为 **mod_labelmaker.c** 的文件。

生成的C文件有点像Apache的“Hello World”。它看起来可能很复杂，但确实提供了一个很长的解释性注释头，值得一读。其思想是，当Apache启动时，位于指定位置且配置为需在服务器配置文件中加载的任何模块都会被加载。`*_register_hooks` 函数列出了在Apache服务器进程的特定阶段可调用的函数名称和签名。在本例中，如果调用了 http://localhost/labelmaker 这个名称，该模块将被要求处理 `*_handler` 函数中发生的任何事情。

服务器的配置可能有点繁琐，但在OpenSuse中，我们必须将其添加到文件 **/etc/apache2/sites-available/default** 中。

```apache
<Location /labelmaker>
    SetHandler labelmaker
</Location>
```

并在 **/etc/sysconfig/apache2** 中，我们**添加**模块 labelmaker 的名称到以下行开头的那一长串逗号分隔的列表中：

```apache
APACHE_MODULES=".....,labelmaker"
```

现在进入labelmaker文件夹并输入：

```bash
sudo apxs2 -c -i mod_labelmaker.c
sudo /etc/init.d/apache2 restart
```

在浏览器中这样调用：

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_67_0.png)

```c
#include "httpd.h"
#include "http_config.h"
#include "http_protocol.h"
#include "ap_config.h"

/* The sample content handler */
static int labelmaker_handler(request_rec *r)
{
    if (strcmp(r->handler, "labelmaker")) {
        return DECLINED;
    }
    r->content_type = "text/html";

    if (!r->header_only) {
        ap_rputs("The sample page from mod_labelmaker.cgi", r);
    }
    return OK;
}

static void labelmaker_register_hooks(apr_pool_t *p)
{
    ap_hook_handler(labelmaker_handler, NULL, NULL, APR_HOOK_MIDDLE);
}

/* Dispatch list for API hooks */
module AP_MODULE_DECLARE_DATA labelmaker_module = {
    STANDARD20_MODULE_STUFF,
    NULL,           /* create per-dir   config structures */
    NULL,           /* merge per-dir    config structures */
    NULL,           /* create per-server config structures */
    NULL,           /* merge per-server config structures */
    NULL,           /* table of config file commands    */
    labelmaker_register_hooks /* register hooks             */
};
```

### 7.2 添加一些功能

现在，我们可以将在第6章中为图形库所做的工作作为替换的处理器函数插入（在代码 Chapter7_1.c 中同时存在两个处理器，其中一个被注释掉了）。注意（高亮的）对修改后的 `decode_value` 函数的调用，它使用 `r->args` 指针来获取QUERY_STRING，而不是 `getenv()`。此外，Apache处理输出的方式也略有不同——你通过调用 `gdImageGifPtr` 获得图像字节数组的指针，然后由 `ap_rwrite` 函数输出数据。在输出调用之后，我们必须使用 `gdFree` 释放该指针。

```c
static int labelmaker_handler(request_rec *r)
{
    void    *iptr;
    int sz = 0;

    if (strcmp(r->handler, "labelmaker")){
        return DECLINED;
    }

    r->content_type = "Content-type: image/gif";

    if (!r->header_only){
        int text=0,background=0, x=0,y=0,size=30,string_rectangle[8];
        double angle=0.0;
        char value[255] = "Hello";
        char font[256] = "/usr/share/fonts/truetype/DejaVuSans.ttf";
        char *err = NULL;
        gdImagePtr im_out = NULL;
        decode_value(r->args, (char *) &value, 255);
        err=gdImageStringFT(NULL,&string_rectangle[0],0,
            font,size,angle,0,0,value);
        x = string_rectangle[2]+string_rectangle[6] + 6;
        y = string_rectangle[3]+string_rectangle[7] + 6;
        im_out = gdImageCreate(x,y);
        background = gdImageColorAllocate(im_out,0,0,0);
        text = gdImageColorAllocate(im_out,255,0,255);
        x = 3 - string_rectangle[6];
        y = 3 - string_rectangle[7];
        err = gdImageStringFT(im_out,&string_rectangle[0],text,
            font,size,angle,x,y,value);
        iptr = gdImageGifPtr(im_out,&sz);
        ap_rwrite(iptr, sz, r);
        gdFree(iptr);
        gdImageDestroy(im_out);
    }
    return OK;
}
```

文件 编辑 查看 历史 书签 工具 帮助

http://localhost/labelmaker?TEXT=The+End+

全书完

