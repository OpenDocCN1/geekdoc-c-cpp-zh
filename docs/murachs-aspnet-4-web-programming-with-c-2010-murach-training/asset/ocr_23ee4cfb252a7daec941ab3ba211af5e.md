# An introduction to SSL

To prevent others from reading data that’s transmitted over the Internet, you can use the Secure Sockets Layer, or SSL. SSL is an Internet protocol that lets you transmit data over the Internet using data encryption. The topics that follow explain how SSL works.

# How secure connections work

Figure 18-1 shows a web page that uses SSL to transfer data between the server and the client over a secure connection. To determine if you’re transmitting data over a secure connection, you can read the URL in the browser’s address bar. If it starts with HTTPS rather than HTTP, then you’re transmitting data over a secure connection.

With a regular HTTP connection, all data is sent as unencrypted text. As a result, if a hacker intercepts this data, it is easy to read. With a secure connection, however, all data that’s transferred between the client and the server is encrypted. Although a hacker can still intercept this data, he won’t be able to read it without breaking the encryption code.

Note that to test an application that uses a secure connection, you must run the application under IIS. Because of that, if you created the application as a file-system web site, you’ll need to use one of the techniques described in chapter 4 to run it under IIS.