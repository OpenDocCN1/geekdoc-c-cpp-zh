```
```java
format.setLenient(false);
JFormattedTextField dateField2 = new JFormattedTextField(format);
dateField2.setValue(new Date());
addRow("Date (short, not lenient):", dateField2);

try
{
    DefaultFormatter formatter = new DefaultFormatter();
    formatter.setOverwriteMode(false);
    JFormattedTextField urlField = new JFormattedTextField(formatter);
    urlField.setValue(new URL("http://java.sun.com"));
    addRow("URL:", urlField);
}
catch (MalformedURLException ex)
{
    ex.printStackTrace();
}

try
{
    MaskFormatter formatter = new MaskFormatter("###-##-####");
    formatter.setPlaceholderCharacter('0');
    JFormattedTextField ssnField = new JFormattedTextField(formatter);
    ssnField.setValue("078-05-1120");
    addRow("SSN Mask:", ssnField);
}
catch (ParseException ex)
{
    ex.printStackTrace();
}

JFormattedTextField ipField = new JFormattedTextField(new IPAddressFormatter());
ipField.setValue(new byte[] { (byte) 130, 65, 86, 66 });
addRow("IP Address:", ipField);
pack();
}

/**
 * Adds a row to the main panel.
 * @param labelText the label of the field
 * @param field the sample field
 */
public void addRow(String labelText, final JFormattedTextField field)
{
    mainPanel.add(new JLabel(labelText));
    mainPanel.add(field);
    final JLabel valueLabel = new JLabel();
    mainPanel.add(valueLabel);
}
```
```