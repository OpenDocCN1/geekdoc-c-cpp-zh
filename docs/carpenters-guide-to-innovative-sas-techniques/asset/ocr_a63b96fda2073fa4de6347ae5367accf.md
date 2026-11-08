```
```xml
<?xml version="1.0" encoding="windows-1252" ?>
- <TABLE>
  - <PATLIST> ③
    <lname>Adams</lname>
    <fname>Mary</fname>
    <sex>F</sex>
    <dob>1951-08-12</dob>
  </PATLIST>
- <PATLIST>
    <lname>Adamson</lname>
    <fname>Joan</fname>
    <sex>F</sex>
    <dob missing="." />
  </PATLIST>
    . . . the remaining observations are not shown . . . .
```
```

② The **libref** TOXML can be used to both read and write the XML file. The name of the data set (PATLIST) is recorded as a part of the XML file ③. This means that multiple SAS data sets can be written to the same XML file.

The selected variables are written to the XML file. Notice that the variables are named on each line and that the date has been re-coded into a YYYY-MM-DD form, and that the missing DOB for ‘Joan Adamson’

has been written using the `missing=` notation.

# SEE ALSO

Hemendinger and Slaughter (2011) briefly describe the use of XML and the XML Mapper.