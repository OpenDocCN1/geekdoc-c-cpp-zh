
## 清单 12.22（续）

```c
else
{
    (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
        "Unsupported value type");
    ret = NULL;
}

free(cret);
RegCloseKey(hkey);
(*env)->ReleaseStringUTFChars(env, name, cname);

return ret;
}

JNIEXPORT void JNICALL Java_Win32RegKey_setValue(JNIEnv* env, jobject this_obj,
    jstring name, jobject value)
{
    const char* cname;
    jstring path;
    const char* cpath;
    HKEY hkey;
    DWORD type;
    DWORD size;
    jclass this_class;
    jclass class_value;
    jclass class_Integer;
    jfieldID id_root;
    jfieldID id_path;
    HKEY root;
    const char* cvalue;
    int ivalue;

    /* get the class */
    this_class = (*env)->GetObjectClass(env, this_obj);

    /* get the field IDs */
    id_root = (*env)->GetFieldID(env, this_class, "root", "I");
    id_path = (*env)->GetFieldID(env, this_class, "path", "Ljava/lang/String;");

    /* get the fields */
    root = (HKEY)(*env)->GetIntField(env, this_obj, id_root);
    path = (jstring)(*env)->GetObjectField(env, this_obj, id_path);
    cpath = (*env)->GetStringUTFChars(env, path, NULL);

    /* open the registry key */
    if (RegOpenKeyEx(root, cpath, 0, KEY_WRITE, &hkey) != ERROR_SUCCESS)
    {
168 if (RegSetValueEx(hkey, cname, 0, type, cvalue, size) != ERROR_SUCCESS)
169 {
170     (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
171         "Set value failed");
172 }
173
174 RegCloseKey(hkey);
175 (*env)->ReleaseStringUTFChars(env, name, cname);
176
177 /* if the value was a string or byte array, release the pointer */
178 if (type == REG_SZ)
179 {
180     (*env)->ReleaseStringUTFChars(env, (jstring) value, cvalue);
181 }
182 else if (type == REG_BINARY)
183 {
184     (*env)->ReleaseByteArrayElements(env, (jarray) value, (jbyte*) cvalue, 0);
185 }
186
187
188 /* helper function to start enumeration of names */
189 static int startNameEnumeration(JNIEnv* env, jobject this_obj, jclass this_class)
190 {
191     jfieldID id_index;
192     jfieldID id_count;
193     jfieldID id_root;
194     jfieldID id_path;
195     jfieldID id_hkey;
196     jfieldID id_maxsize;
197
198     HKEY root;
199     jstring path;
200     const char* cpath;
201     HKEY hkey;
202     DWORD maxsize = 0;
203     DWORD count = 0;
204
205     /* get the field IDs */
206     id_root = (*env)->GetFieldID(env, this_class, "root", "I");
207     id_path = (*env)->GetFieldID(env, this_class, "path", "Ljava/lang/String;");
208     id_hkey = (*env)->GetFieldID(env, this_class, "hkey", "I");
209     id_maxsize = (*env)->GetFieldID(env, this_class, "maxsize", "I");
210     id_index = (*env)->GetFieldID(env, this_class, "index", "I");
211     id_count = (*env)->GetFieldID(env, this_class, "count", "I");
212
213     /* get the field values */
214     root = (HKEY) (*env)->GetIntField(env, this_obj, id_root);
215     path = (jstring)(*env)->GetObjectField(env, this_obj, id_path);
236    cpath = (*env)->GetStringUTFChars(env, path, NULL);
238    /* open the registry key */
239    if (RegOpenKeyEx(root, cpath, 0, KEY_READ, &hkey) != ERROR_SUCCESS)
240    {
241        (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
242                         "Open key failed");
243        (*env)->ReleaseStringUTFChars(env, path, cpath);
244        return -1;
245    }
246    (*env)->ReleaseStringUTFChars(env, path, cpath);
248    /* query count and max length of names */
249    if (RegQueryInfoKey(hkey, NULL, NULL, NULL, NULL, NULL, NULL, &count, &maxsize,
250                        NULL, NULL, NULL) != ERROR_SUCCESS)
251    {
252        (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
253                         "Query info key failed");
254        RegCloseKey(hkey);
255        return -1;
256    }
258    /* set the field values */
259    (*env)->SetIntField(env, this_obj, id_hkey, (DWORD) hkey);
260    (*env)->SetIntField(env, this_obj, id_maxsize, maxsize + 1);
261    (*env)->SetIntField(env, this_obj, id_index, 0);
262    (*env)->SetIntField(env, this_obj, id_count, count);
263    return count;
264 }
265 JNIEXPORT jboolean JNICALL Java_Win32RegKeyNameEnumeration_hasMoreElements(JNIEnv* env,
266        jobject this_obj)
267 {
268     jclass this_class;
269     jfieldID id_index;
270     jfieldID id_count;
271     jint index;
272     jint count;
273     /* get the class */
274     this_class = (*env)->GetObjectClass(env, this_obj);
276     /* get the field IDs */
277     id_index = (*env)->GetFieldID(env, this_class, "index", "I");
278     id_count = (*env)->GetFieldID(env, this_class, "count", "I");
280     index = (*env)->GetIntField(env, this_obj, id_index);
281     if (index == -1) /* first time */
282     {
        count = startNameEnumeration(env, this_obj, this_class);
        index = 0;
    }
    else
        count = (*env)->GetIntField(env, this_obj, id_count);
    return index < count;
}

JNIEXPORT jobject JNICALL Java_Win32RegKeyNameEnumeration_nextElement(JNIEnv* env,
        jobject this_obj)
{
    jclass this_class;
    jfieldID id_index;
    jfieldID id_hkey;
    jfieldID id_count;
    jfieldID id_maxsize;

    HKEY hkey;
    int index;
    int count;
    DWORD maxsize;

    char* cret;
    jstring ret;

    /* get the class */
    this_class = (*env)->GetObjectClass(env, this_obj);

    /* get the field IDs */
    id_index = (*env)->GetFieldID(env, this_class, "index", "I");
    id_count = (*env)->GetFieldID(env, this_class, "count", "I");
    id_hkey = (*env)->GetFieldID(env, this_class, "hkey", "I");
    id_maxsize = (*env)->GetFieldID(env, this_class, "maxsize", "I");

    index = (*env)->GetIntField(env, this_obj, id_index);
    if (index == -1) /* first time */
    {
        count = startNameEnumeration(env, this_obj, this_class);
        index = 0;
    }
    else
        count = (*env)->GetIntField(env, this_obj, id_count);

    if (index >= count) /* already at end */
    {
        (*env)->ThrowNew(env, (*env)->FindClass(env, "java/util/NoSuchElementException"),
                "past end of enumeration");
        return NULL;
    }
332    maxsize = (*env)->GetIntField(env, this_obj, id_maxsize);
333    hkey = (HKEY) (*env)->GetIntField(env, this_obj, id_hkey);
334    cret = (char*)malloc(maxsize);

336    /* find the next name */
337    if (RegEnumValue(hkey, index, cret, &maxsize, NULL, NULL, NULL, NULL) != ERROR_SUCCESS)
338    {
339       (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
340          "Enum value failed");
341       free(cret);
342       RegCloseKey(hkey);
343       (*env)->SetIntField(env, this_obj, id_index, count);
344       return NULL;
345    }

348    ret = (*env)->NewStringUTF(env, cret);
349    free(cret);

351    /* increment index */
352    index++;
353    (*env)->SetIntField(env, this_obj, id_index, index);

355    if (index == count) /* at end */
356    {
357       RegCloseKey(hkey);
358    }

360    return ret;
361 }
```

## 清单 12.23 `win32reg/Win32RegKeyTest.java`

```java
1   import java.util.*;
2
3   /**
4    * @version 1.02 2007-10-26
5    * @author Cay Horstmann
6    */
7   public class Win32RegKeyTest
8   {
9      public static void main(String[] args)
10     {
11        Win32RegKey key = new Win32RegKey(
12           Win32RegKey.HKEY_CURRENT_USER, "Software\\JavaSoft\\Java Runtime Environment");
13
14        key.setValue("Default user", "Harry Hacker");
15        key.setValue("Lucky number", new Integer(13));
16        key.setValue("Small primes", new byte[] { 2, 3, 5, 7, 11 });
17
18        Enumeration<String> e = key.names();
19
20        while (e.hasMoreElements())
21        {
22            String name = e.nextElement();
23            System.out.print(name + "=");
24
25            Object value = key.getValue(name);
26
27            if (value instanceof byte[])
28                for (byte b : (byte[]) value) System.out.print((b & 0xFF) + " ");
29            else
30                System.out.print(value);
31
32            System.out.println();
33        }
34     }
35  }
```

- **类型查询函数**
  - `boolean IsAssignableFrom(JNIEnv *env, jclass cl1, jclass cl2)` 如果第一个类的对象可以赋值给第二个类的对象，则返回 `JNI_TRUE`，否则返回 `JNI_FALSE`。此函数测试这些类是否相同，或者 `cl1` 是 `cl2` 的子类，或者 `cl2` 表示由 `cl1` 或其某个超类实现的接口。
  - `jclass GetSuperclass(JNIEnv *env, jclass cl)` 返回一个类的超类。如果 `cl` 表示类 `Object` 或一个接口，则返回 `NULL`。

现在你已经到达了 *Java 核心技术* 第二卷的末尾，完成了一段漫长的旅程，在其中你遇到了许多高级 API。我们从每个 Java 程序员都需要了解的主题开始：流、XML、网络、数据库和国际化。三个长章节涵盖了图形和 GUI 编程。最后，我们以非常技术性的章节结束，涉及安全、远程方法、注解处理和本地方法。我们希望你喜欢这次穿越 Java API 广阔领域的旅程，并希望你能将新获得的知识应用到你的项目中。
