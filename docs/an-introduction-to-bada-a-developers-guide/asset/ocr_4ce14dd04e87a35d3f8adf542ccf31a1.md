```
xmlFreeDoc(docPtr);
return;
}

if (xmlStrcmp(curNodePtr->name, (const xmlChar*) "notes_get_response"))
{
    xmlFreeDoc(docPtr);
    return;
}
```

To get the root element call the xmlDocGetRootElement() function, which takes the xmlDocPtr and returns the document pointer. To compare the node value use the xmlStrcmp() function. This returns true if the node name matches. Using this function compare the root element pointer with the root node string.

+   3. Now get all the child nodes of the root node and traverse them one by one to the ‘note’ node.

```
curNodePtr = curNodePtr->xmlChildrenNode;

while (curNodePtr != NULL)
{
    if (!xmlStrcmp(curNodePtr->name, (const xmlChar*) "note"))
        GetNoteData(docPtr, curNodePtr);

    curNodePtr = curNodePtr->next;
}
```

+   4. Use the curNodePtr to get the value under the ‘note’ tag.

```
void
GetNoteData(xmlDocPtr doc, xmlNodePtr cur)
{
    xmlChar* keyTitle = null;
    xmlChar* keyContent = null;

    cur = cur->xmlChildrenNode;

    while (cur != null)
    {
        // Get Title tag data
        if (!xmlStrcmp(cur->name, (const xmlChar*) "title"))
            keyTitle = xmlNodeListGetString(doc, cur->xmlChildrenNode, 1);

        // Get Content Tag Data
```