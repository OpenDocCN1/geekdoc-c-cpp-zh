# Listing 11.24 _(Continued)_

```
```java
67    catch (IOException ex)
68    {
69        ex.printStackTrace();
70    }
71    });
72
73    printButton.addActionListener(event ->
74    {
75        try
76        {
77            Desktop.getDesktop().print(chooser.getSelectedFile());
78        }
79        catch (IOException ex)
80        {
81            ex.printStackTrace();
82        }
83    });
84
85    browseButton.addActionListener(event ->
86    {
87        try
88        {
89            Desktop.getDesktop().browse(new URI(browseField.getText()));
90        }
91        catch (URISyntaxException | IOException ex)
92        {
93            ex.printStackTrace();
94        }
95    });
96
97    mailButton.addActionListener(event ->
98    {
99        try
100       {
101           String subject = percentEncode(subjectField.getText());
102           URI uri = new URI("mailto:" + toField.getText() + "?subject=" + subject);
103
104           System.out.println(uri);
105           Desktop.getDesktop().mail(uri);
106       }
107       catch (URISyntaxException | IOException ex)
108       {
109           ex.printStackTrace();
110       }
111   });
112
```
```