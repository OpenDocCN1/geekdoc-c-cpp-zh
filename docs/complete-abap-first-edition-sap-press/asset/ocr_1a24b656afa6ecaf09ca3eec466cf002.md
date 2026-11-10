```
```text
* Create 'XML object
lr_xml = cl_xml=>create( ).
*Create Document
lr_document = lr_xml->create_document( ).
*Create encoding
lr_encoding = lr_xml->create_encoding( BYTE_ORDER = 0 CHARACTER_SET =
 'UTF-8').
*Set encoding
lr_document->set_encoding( lr_encoding ).
*Create element "extension" as root
lr_extension = lr_document->create_simple_element(
name = 'extension'
parent = lr_document ).
*Set attribute for the "extension" element
lr_extension->set_attribute( name = 'Type'
VALUE = 'Component' ).
*Create "files" element with "extension" element as parent
lr_files = lr_document->create_simple_element(
name = 'files'
parent = lr_extension ).
*Set attribute for "files" element
lr_files->set_attribute( name = 'Folder'
VALUE = 'site' ).
*Create element content
lr_document->create_simple_element( name = 'filename'
parent = lr_files
VALUE = 'index.html' ).
lr_document->create_simple_element( name = 'filename'
parent = lr_files
VALUE = 'site.php' ).

*Create "media" element with "extension" element as parent
lr_media = lr_document->create_simple_element(
name = 'media'
parent = lr_extension ).
**Set attribute for "media" element
lr_media->set_attribute( name = 'Folder'
VALUE = 'media' ).

*Create element content
lr_document->create_simple_element( name = 'folder'
parent = lr_media
VALUE = 'css' ).
lr_document->create_simple_element( name = 'folder'
parent = lr_media
VALUE = 'images' ).
lr_document->create_simple_element( name = 'folder'
parent = lr_media
VALUE = 'js' ).
```
```