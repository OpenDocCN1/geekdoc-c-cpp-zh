```
```java
178    }
179    return obj;
180  }
181  catch (Exception ex) // the reflection methods can throw various exceptions
182  {
183    ex.printStackTrace();
184    return null;
185  }
186 }
187
188 /**
189  * Parses a value element.
190  * @param e a value element
191  */
192 private Object parseValue(Element e)
193 {
194   Element child = (Element) e.getFirstChild();
195   if (child.getTagName().equals("bean")) return parseBean(child);
196   String text = ((Text) child.getFirstChild()).getData();
197   if (child.getTagName().equals("int")) return new Integer(text);
198   else if (child.getTagName().equals("boolean")) return new Boolean(text);
199   else if (child.getTagName().equals("string")) return text;
200   else return null;
201 }
202 }
```
```

# **Listing 3.4** read/fontdialog.xml

```
```xml
1 <?xml version="1.0"?>
2 <!DOCTYPE gridbag SYSTEM "gridbag.dtd">
3 <gridbag>
4   <row>
5     <cell anchor="EAST">
6       <bean>
7         <class>javax.swing.JLabel</class>
8         <property>
9           <name>text</name>
10          <value>string-face: </string></value>
11        </property>
12      </bean>
13    </cell>
14    <cell fill="HORIZONTAL" weightx="100">
15      <bean id="face">
16        <class>javax.swing.JComboBox</class>
17      </bean>
18    </cell>
19    <cell gridheight="4" fill="BOTH" weightx="100" weighty="100">
20      <bean id="sample">
```
```