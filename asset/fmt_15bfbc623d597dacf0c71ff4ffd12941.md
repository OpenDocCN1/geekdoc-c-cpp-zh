
# 第 7 章 使用外部数据

## 使用外部数据

另一种用于传输数据的格式正变得越来越流行，即 JSON（JavaScript 对象表示法）。JSON 是一种数据交换的开放标准。许多人认为它优于 XML 的优势在于其传输开销比 XML 小得多。例如，一对标签可能占用 20 字节，而同样的界定在 JSON 中只需少量的字节即可完成。JSON 不像 XML 那样使用单个根元素，而是使用一对大括号。JSON 不使用标签来指定字段，而是使用用冒号分隔的键-值对。键名和值被包含在自己的引号中。包含在大括号内的内容被称为“对象”（object），类似于我们在数据表中可能指称的“记录”（record）。

数组（array）或一系列相似的键-值对由一对方括号界定。例如，让我们取之前使用的 XML 示例并用 JSON 记法重新开始。首先，是原始的 XML 记法。

```xml
<?xml version="1.0"?>
<person>
<name>
<first>Jim</first>
<last>Sheusi</last>
</name>
<occupation>College Professor</occupation>
<position>Dept. Chair</position>
</person>
```

接下来，是用 JSON 实现相同的内容。

```json
{
"name":{
"first":"Jim",
"last":"Sheusi"
},
"occupation":"College Professor",
"position":"Dept. Chair"
}
```

一眼看出，不含空格的 JSON 版本字符数为 95，而相同数据在 XML 中为 159。这使得 JSON 与 XML 相比效率提高了约 50%。

为了执行与之前相同的练习，但仅使用 JSON 作为接收服务器返回结果的格式，我们首先需要在源码中添加以下包和类：`org.json.*` 和 `java.util.Iterator`。

接下来，修改你的内部线程如下：

```java
private class Background extends Thread {
    String devout;
    String rawdata="";
    HashMap<String, String> hm = new HashMap<String, String>();

    public Background(String devout) {
        this.dev = devout;
    }

    public HashMap<String, String> retrieveResponse() {
        return hm;
    }

    public String retrieveRawData() {
        return rawdata;
    }

    public void run() {
        // getXMLData();
        getJSONData();
    }

    public void getJSONData() {
        String querystring = "http://tageninformatics.com/client/sheusi/data.php?encoding=json&" + devout;
        try {
            URL myUrl = new URL(querystring);
            HttpURLConnection myConnection = (HttpURLConnection)myUrl.openConnection();
            InputStreamReader isr = new InputStreamReader(myConnection.getInputStream(),"UTF-8");
            BufferedReader reader = new BufferedReader(isr);
            StringBuilder sb = new StringBuilder();
            for (String line=null; line = reader.readLine())!=null; {
                sb.append(line).append("\n");
            }
            rawdata=sb.toString();
            JSONObject data = new JSONObject(sb.toString()); // 对象
            Iterator keys = data.keys();
            while (keys.hasNext()) {
                String key = (String) keys.next();
                String value = data.getString(key);
                hm.put(key, value);
            }
        } catch (JSONException je) {
            Log.i("info", "json error");
        } catch (MalformedURLException male) {
            Log.i("info", "bad URL");
        } catch (IOException ioe) {
            Log.i("info", "some error");
        }
    }

    public void getXMLData() {
        String querystring = "http://tageninformatics.com/client/sheusi/data.php?encoding=xml&" + devout;
        try {
            URL myUrl = new URL(querystring);
            HttpURLConnection myConnection = (HttpURLConnection)myUrl.openConnection();
            InputStreamReader isr = new InputStreamReader(myConnection.getInputStream(), "UTF-8");
            BufferedReader br = new BufferedReader(isr);
            StringBuilder sb = new StringBuilder();
            for (String line = null; (line = br.readLine()) != null;) {
                sb.append(line).append("\n");
            }
            rawData=sb.toString();
            XMLPullParserFactory factory = XMLPullParserFactory.newInstance();
            XMLPullParser parser = factory.newPullParser();
            parser.setInput(new StringReader(sb.toString()));
            int event;
            while ((event = parser.next()) != -1) {
                if (event == XMLPullParser.START_TAG) {
                    String tagName = parser.getName();
                    if (tagName.equals("email")) {
                        icd.setText(parser.getTextText());
                    } else if (tagName.equals("lname")) {
                        hm.put("lname", parser.getTextText());
                    } else if (tagName.equals("fname")) {
                        hm.put("fname", parser.getTextText());
                    } else if (tagName.equals("address")) {
                        hm.put("address", parser.getTextText());
                    } else if (tagName.equals("city")) {
                        hm.put("city", parser.getTextText());
                    } else if (tagName.equals("state")) {
                        hm.put("state", parser.getTextText());
                    } else if (tagName.equals("zip")) {
                        hm.put("zip", parser.getTextText());
                    }
                }
            }
            icd.setText(rawData);
        } catch (Exception e) {
            Log.info("info".XML error);
        }
    }
}
```

```java
rawData = sb.toString();
try {
    XmlPullParserFactory factory = XmlPullParserFactory.newInstance();
    factory.setNamespaceAware(true);
    XmlPullParser xpp = factory.newPullParser();
    StringReader sr = new StringReader(rawData);
    xpp.setInput(sr);
    String currenttag = "*";
    xpp.next(); // 跳过 XML 中的描述符行
    // 输入
    int eventType = xpp.getEventType(); // 这些整数将以符号常量的形式出现
    while (eventType != XmlPullParser.END_DOCUMENT) {
        if (eventType == XmlPullParser.START_DOCUMENT) {
            // 什么都不做
        }
        if (eventType == XmlPullParser.START_TAG) {
            currenttag = xpp.getName();
        }
        if (eventType == XmlPullParser.TEXT) {
            hm.put(currenttag, xpp.getText());
        }
        if (eventType == XmlPullParser.END_TAG) {
            // 什么都不做
        }
        eventType = xpp.next(); // 继续执行
    } // 结束 while
} catch (XmlPullParserException mppe) {
} catch (MalformedURLException male) {
} catch (IOException ioe) {
}
// 结束 run()
// 结束内部类
@Override
public void onStop() {
    super.onStop();
    this.finish();
}
```

```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getInflater().inflate(R.menu.activity_main, menu);
}
```

当应用程序运行时，你应该能看到如图 7.1 所示的显示。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_225_0.png)

**图 7.1** Toshiba Thrive 在竖屏模式下运行来自 PHP 应用程序的 XML。
: Google.
