```
<content>chamber of secrets :)</content>
<created_time>1271379740</created_time>
<updated_time>1271379740</updated_time>
<uid>100000951206325</uid>
<content_html>chamber of secrets :)</content_html>
</note>

<note>
<note_id>11459818561982</note_id>
<title>...</title>
<content>Man without aim is letter without address .</content>
<created_time>1271297013</created_time>
<updated_time>1271297013</updated_time>
<uid>100000951206325</uid>
<content_html>Man without aim is letter without address.</content_html>
</note>

<note>
<note_id>114054615281169</note_id>
<title>Sayings</title>
<content>No dream comes true unless U wake up and work for it !!</content>
<created_time>12711138928</created_time>
<updated_time>12711138928</updated_time>
<uid>100000951206325</uid>
<content_html>No dream comes true unless U wake up and work for it !!</content_html>
</notes_get_response>
```

Below are the detailed steps for parsing the XML received in response to GetNotes:

+   1. Load the XML buffer into DOM parser.

```
xmlDocPtr docPtr = null;
xmlNodePtr curNodePtr = null;

docPtr = xmlParseDoc((unsigned char*)pBuf->GetPointer());

if (docPtr == NULL)
{
    return;
}
```

Here, pBuf is the buffer that contains the response XML from the GetNotes request to Facebook. xmlParseDoc() parses the buffer containing the XML data and returns an XmlDocPtr, which organises the data into a tree to make it easier to parse the individual elements.

+   2. Get the root element of XML. In this example, the XML root element is “notes_get_response”.

```
curNodePtr = xmlDocGetRootElement(docPtr);

if (curNodePtr == NULL)
{
```