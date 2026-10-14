# How to add an attachment to an email message

An *attachment* is a file that’s sent along with an email message. The most common types of attachments are text files, word processing documents, spreadsheets, pictures, and other media files such as sound and video files.

Figure 20-5 shows how you can create an attachment and add it to an email message. After you create an attachment object using the Attachment class, you add the object to the mail message’s Attachments collection. Then, you can send the message.

Since SMTP protocol is designed to send text messages, not binary files, any email attachment for a binary file must be converted to text format before it can be sent. Then, the text attachment must be converted back to a binary file when it’s received. The most common format for converting attached binary files to text and back to binary is called *UUEncode*, and it’s used by default. The other available format for converting binary files is called *Base64*. Since you shouldn’t need to use this format, I haven’t shown you how to create an attachment that uses it here.