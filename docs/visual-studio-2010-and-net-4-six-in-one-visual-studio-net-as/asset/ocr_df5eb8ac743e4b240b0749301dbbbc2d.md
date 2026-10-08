# LISTING 20-14 (continued)

```
<asp:Label ID="Throbber" runat="server" Style="display: none">
<img src="Images/UploadIndicator.gif" align="asmidsmidble"
alalt="loading" />
</asp:label>
<br />
<br />
<asp:Label ID="StatusLabel" runat="server" />
</ContentTemplate>
</asp:UpdatePanel>
</div>
</form>
<body>
</html>
```

Code file[AsyncFileUploadSample.aspx] available for download at Wrox.com

The AsyncFileUpload control in the page sets up several properties. Table 20-6 summarizes the properties you can use with the control.

| PROPERTY | DESCRIPTION |
| --- | --- |
| CompleteBackColor | The control's background color to set when upload has completed. |
| ContentType | Gets the MIME content type of a file sent by a client. |
| ErrorBackColor | The control's background color to set when an upload error occurs. |
| FileContent | Gets a Stream object that points to an upload file to prepare for reading the contents of the file. |
| FileName | Gets the name of a file on a client to upload using the control. |
| HasFile | Gets a flag indicating whether the control contains a file. |
| OnClientUploadComplete | The name of a JavaScript function executed on the client side after the file is successfully uploaded. |
| OnClientUploadError | The name of a JavaScript function executed on the client side if the file uploading failed. |
| OnClientUploadStarted | The name of a JavaScript function executed on the client side on the file uploading started. |
| PostedFile | Gets an HttpPostedFile object that provides access to the uploaded file. |