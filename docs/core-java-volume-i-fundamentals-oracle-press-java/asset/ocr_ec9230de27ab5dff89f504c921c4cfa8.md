```
```java
156
157             public void write(byte[] b, int off, int len)
158             {
159                 output.append(new String(b, off, len));
160             }
161         });
162     }
163
164     public void publish(LogRecord record)
165     {
166         if (!frame.isVisible()) return;
167         super.publish(record);
168         flush();
169     }
170 }
```
```

# **java.util.logging.Logger** 1.4

+   - `Logger getLogger(String loggerName)`
+   - `Logger getLogger(String loggerName, String bundleName)`
+   
+     gets the logger with the given name. If the logger doesn’t exist, it is created. Localized messages are located in the resource bundle whose name is bundleName.
+   - `void severe(String message)`
+   - `void warning(String message)`
+   - `void info(String message)`
+   - `void config(String message)`
+   - `void fine(String message)`
+   - `void finer(String message)`
+   - `void finest(String message)`
+   
+     logs a record with the level indicated by the method name and the given message.