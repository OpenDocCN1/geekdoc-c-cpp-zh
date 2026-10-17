```
```cpp
if ( value != 0 ){
   cout << value;
}else{
   cout << "Environment variable does not exist.";
}
cout << "</td></tr>\n";
}
cout << "</table>\n";
cout << "</body>\n";
cout << "</html>\n";

return 0;
}
```
```

The output is as follows:

| Environment variable | Value |
|---|---|
| COMSPEC | Environment variable does not exist. |
| DOCUMENT_ROOT | /var/www/tutorialspoint |
| GATEWAY_INTERFACE | CGI/1.1 |
| HTTP_ACCEPT | text/html, application/xhtml+xml, */* |
| HTTP_ACCEPT_ENCODING | gzip, deflate |
| HTTP_ACCEPT_LANGUAGE | en-US |
| HTTP_CONNECTION | Keep-Alive |
| HTTP_HOST | www.tutorialspoint.com |
| HTTP_USER_AGENT | Mozilla/5.0 (Windows NT 6.3; WOW64; Trident/7.0; rv:11.0) like Gecko |
| PATH | /sbin:/usr/sbin:/bin:/usr/bin |
| QUERY_STRING |  |
| REMOTE_ADDR | 183.82.104.71 |
| REMOTE_PORT | 50902 |
| REQUEST_METHOD | GET |
| REQUEST_URI | /cgi-bin/cpp_env.cgi |
| SCRIPT_FILENAME | /var/www/cgi-bin/cpp_env.cgi |
| SCRIPT_NAME | /cgi-bin/cpp_env.cgi |
| SERVER_ADDR | 66.135.33.172 |