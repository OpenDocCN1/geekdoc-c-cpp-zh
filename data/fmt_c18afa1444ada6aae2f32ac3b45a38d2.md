
当传递 null 访问控制上下文时，两个参数的 `doPrivileged()` 方法无法将上下文降低到之前保存的上下文的水平。因此，当 `accessControlContext` 参数为 null 时，此代码可能会授予过度权限。意图使用 null 访问控制上下文调用 `AccessController.doPrivileged()` 的程序员应显式传递 null 常量，或使用单参数版本的 `AccessController.doPrivileged()`。

### 合规解决方案

此合规解决方案通过确保 `accessControlContext` 不空来防止授予过度权限：

```java
if (accessControlContext == null) {
  throw new SecurityException("Missing AccessControlContext");
}
AccessController.doPrivileged(
  new PrivilegedAction<Void>() {
    public Void run() {
      // ...
    }
}, accessControlContext);
```

## 5. 防止任意文件上传

参数。如果将意外的参数值传递给安全敏感型方法，就可能导致任意代码执行，并可能引发权限提升。

[API 2013] `AccessController.doPrivileged()`, `System.setSecurityManager()`

### 5. 防止任意文件上传

接受文件上传的 Java 应用程序（包括 Web 应用）必须确保攻击者无法上传或传输恶意文件。如果目标系统执行了包含代码的受限制文件，可能会破坏应用层的防御。例如，允许上传 HTML 文件的应用程序可能会允许恶意代码的执行——在缺少输出转义程序的情况下，攻击者可以提交一个带有跨站脚本（XSS）负载字段的有效 HTML 文件。出于此原因，许多应用程序限制了可以上传的文件类型。

可能会上传具有 `.exe` 和 `.sh` 等危险扩展名的文件，这可能导致服务器端应用程序的任意代码执行。仅限制 HTTP 请求头中 `Content-Type` 字段的应用程序可能会受到此类攻击。

为了支持文件上传，一个典型的 Java Server Pages (JSP) 页面通常包含如下代码：

```
<form action="doUpload" method="POST"
ctype="multipart/form-data">
<file name="uploadFile" label="Choose File" size="40" />
<submit value="Upload" name="submit" />
</form>
```

许多企业框架提供了配置设置，旨在作为防止任意文件上传的防御。遗憾的是，大多数未能提供足够的保护。缓解此漏洞涉及检查文件大小、内容类型和文件内容以及其他元数据属性。

### 不合规代码示例

此合规代码示例显示了 Struts 2 应用程序上传操作中的 XML 代码。拦截器负责允许文件上传。

#### 14 章 第1 章 安全

```
<action name="doUpload" class="com.example.UploadAction">
  <interceptor-ref name="fileUpload">
    <param name="maximumSize">10240</param>
    <param name="allowedTypes">
      text/plain,image/JPEG,text/html
    </param>
  </interceptor-ref>
</action>
```

文件上传代码出现在 `UploadAction` 类中：

```java
public class UploadAction extends ActionSupport {
  private File uploadedFile;
  // setter and getter for uploadedFile

  public String execute() {
    try {
      // 为了演示，路径和文件名硬硬编码
      File fileCreate = new File("filepath", "filename");
      // 将文件内容拷贝到此处
      FileUtils.copyFile(uploadedFile, fileToFile);
      return "SUCCESS";
    } catch (Throwable e) {
      addActionError(e.getMessage());
      return "ERROR";
    }
  }
}
```

参数类型 `maxSize` 的值确保特定的 Action 无法接收大文件。`allowedTypes` 参数定义了接受的文件类型。然而，这种方法无法确保上传的文件符合安全要求，因为拦截器检查可以被轻易绕过。如果攻击者使用代理工具更改传输过程中原始 HTTP 请求中的内容类型，框架将无法阻止文件的上传。因此，攻击者可以上传一个具有 `.exe` 扩展名的恶意文件（例如）。

### 合规解决方案

只有当内容类型与文件的实际内容匹配时，文件上传才能成功。例如，具有图像头的文件必须只包含图像，且不能包含可执行代码。此合规解决方案使用 Apache Tika 库 [Apache 2013] 利用现有的解析器库检测并提取文档中的元数据和结构化文本内容。在调用 `execute()` 中负责上传文件的代码之前，必须调用 `checkMetaData()` 方法。

```java
public class UploadAction extends ActionSupport {
    private File uploadedFile;
    // setter and getter for uploadedFile

    public String execute() {
        try {
            // 为了演示，路径和文件名硬编码
            File fileToFileCreate = new File("filepath", "filename");

            boolean textPlain = checkMetaData(uploadedFile,
                "text/plain");
            boolean img = checkMetaData(uploadedFile, "image/JPEG");
            boolean textHtml = checkMetaData(uploadedFile,
                "text/html");

            if (!textPlain || !img || !textHtml) {
                return "ERROR";
            }

            // 将临时文件内容拷贝到此处
            FileUtils.copyFile(uploadedFile, fileToFileCreate);
            return "SUCCESS";
        } catch (Throwable e) {
            addActionError(e.getMessage());
            return "ERROR";
        }
    }

    public static boolean checkMetaData(
        File f, String contentType) {
        try (InputStream is = new FileInputStream(f)) {
            ContentHandler contenthandler = new ContentHandler();
            metadata.set(Metadata.RESOURCE_KEY, f.getName());
            Parser parser = new AutoDetectParser();
            try {
                parser.parse(is, contenthandler,
                    metadata, new ParseContext());
            } catch (SAXException | ParserException e) {
                // 处理错误
                return false;
            }
            if (metadata.get(Metadata.CONTENT_TYPE).equalsIgnoreCase(
            contentType)) {
                return true;
            } else {
                return false;
            }
        } catch (IOException e) {
            // 处理错误
            return false;
        }
    }
```

`AutoDetectParser` 根据文件的内容类型选择最佳可用解析器。

### 适用性

任意上传漏洞可能导致权限提升和任意代码执行。

+   [Apache 2013] Apache Tika: Content Analysis Toolkit

## 6. 对输出进行适当编码或转义

存在多个用于输出数据的系统。输出系统的数据可能源于可信源。然而，假设输出清理是不必要的危险的，因为数据可能直接源于不可信源并包含恶意内容。例如，HTML 渲染器容易受到 HTML 注入和跨站脚本（XSS）攻击 [OWASP 2011]。防止此类攻击的输出清理与输入清理同样重要。

与输入一样，数据在清理之前应进行归一化。对除已知安全的字符外的所有输出进行正确编码，以避免由绕过验证导致的漏洞。详见《Java 安全编码标准》[Long 2012]，“IDS01-J. 在验证之前对字符串进行归一化”。

### 不合规代码示例

此合规代码示例使用基于 Java EE 的 Spring 框架的模型视图控制器（MVC）概念在不进行编码或转义的情况下向用户显示数据。由于数据被发送到 Web浏览器，该代码受到 HTML 注入和 XSS 攻击。

```java
@RequestMapping("/notifications.htm")
public ModelAndView getNotifications(
    HttpServletRequest request, HttpServletResponse response) {
    ModelAndView mv = new ModelAndView();
    try {
        UserInfo userDetails = getUserInfo();
        List<Map<String, Object>> list = 
            new ArrayList<Map<String, Object>>();
        List<Notification> notificationList = 
            notificationService.getNotificationsForUserId(
            userDetails.getPersonId());
        
        for (Notification notification : notificationList) {
            Map<String, Object> map = new HashMap<String, Object>();
            map.put("id", notification.getId());
            map.put("message", notification.getMessage());
            list.add(map);
        }

        mv.addObject("Notifications", list);
    } catch (Throwable t) {
        // 记录到文件并处理
    }

    return mv;
}
```

### 合规解决方案

此合规解决方案定义了一个 `ValidationError` 类，将输出归一化为已知字符，使用白名单执行输出清理并对任何未指定的数据值进行编码以实施双重检查机制 [OWASP 2013]。

```java
public class ValidateOutput {
    // 允许字母、数字和空格
    private static final Pattern pattern = Pattern.compile("^[a-zA-Z0-9-\\s]{0,20}$");

    // 根据白名单对输入字段进行验证和编码
    public String validate(String name, String input)
        throws ValidationException {
        String canonical = normalize(input);

        if (!pattern.matcher(canonical).matches()) {
            throw new ValidationException("Improper format in " + name + " field");
        }

        // 对无效字符执行输出编码
        canonical = HTMLEntityEncode(canonical);
        return canonical;
    }

    // 规范化为已知实例
    private static String normalize(String input) {
        String canonical = java.text.Normalizer.normalize(input, Normalizer.Form.NFKC);
        return canonical;
    }

    // 编码无效数据
    private static String HTMLEntityEncode(String input) {
        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < input.length(); i++) {
            char ch = input.charAt(i);
            if (Character.isLetterOrDigit(ch) || Character.isWhitespace(ch)) {
                sb.append(ch);
            } else {
                sb.append("&#" + (int)ch + ";");
            }
        }
        return sb.toString();
    }
}
```

### 6. 正确编码或转义输出

```java
// ...

@RequestMapping("/getnotifications.htm")
public ModelAndView getNotifications(HttpServletRequest request, 
    HttpServletResponse response) {
    ValidateOutput vo = new ValidateOutput();

    ModelAndView mv = new ModelAndView();
    try {
        UserInfo userDetails = getUserInfo();
        List<Map<String, Object>> list = new ArrayList<Map<String, Object>>();
        NotificationList notificationList = notificationService.getNotificationsForUserId(
            userDetails.getUserId());

        for (Notification notification : notificationList) {
            Map<String, Object> map = new HashMap<String, Object>();
            map.put("id", vo.validate("id", notification.getId()));
            map.put("message", 
                vo.validate("message", notification.getMessage()));
            list.add(map);
        }

        mv.addObject("Notifications", list);
    } catch (Throwable t) {
        // 记录日志到文件并处理
    }

    return mv;
}
```
