# Video Transcode Scheduling for MPEG-DASH in Cloud Environments ■ 109

TABLE 5.2 The XML Syntax of the Hierarchical Data Model

```
<<!-- MPD Type- >
<xs:complexType name = "MPDtype">
  <xs:sequence>
    <xs:element name = "ProgramInformation"
      type = "ProgramInformation" minOccurs = "0"/>
    <xs:element name = "Period" type = "PeriodType"
      maxOccurs = "unbounded"/>
    <xs:element name = "BaseURL" type = "BaseURLType"
      minOccurs = "0" maxOccurs = "unbounded"/>
    <xs:any namespace = "##" processContents
      minOccurs = "lax" maxOccurs = "unbounded"/>
  </xs:sequence>
  <xs:attribute name = "profiles" type = "URIVectorType"/>
  <xs:attribute name = "type" type = "PresentationType"
    default = "OnDemand"/>
  <xs:attribute name = "availabilityStartTime" type = "xs:dateTime"/>
  <xs:attribute name = "availabilityEndTime" type = "xs:dateTime"/>
  <xs:attribute name = "mediaPresentationDuration"
    type = "duration"/>
  <xs:attribute name = "minimumUpdatePeriodMPD"
    type = "duration"/>
  <xs:attribute name = "minBuffer" type = "xs:duration"/>
  <xs:attribute name = "shiftBufferDepth" type = "xs:duration"/>
  <xs:any namespace = "##" processContents = "lax"/>
</xs:complexType>
```

```
<<!-- Type of presentation - live or on-demand- >
<xs:simpleType name = "PresentationType">
  <xs:restriction base = "xs:string">
    <xs:enumeration value = "OnDemand"/>
    <xs:enumeration value = "Live"/>
  </xs:restriction>
</xs:simpleType>
<!-- Supplementary URL to the one given as attribute- >
<xs:complexType name = "BaseURLType">
  <xs:simpleContent>
    <xs:extension base = "xs:anyURI">
      <xs:any namespace = "##"
        processContents = "lax"/>
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

```
<<!-- Type of space delimited list of URIS- >
<xs:simpleType name = "URIVectorType">
  <xs:list itemType = "xs:anyURI"/>
</xs:simpleType>
```