| java.net.HttpRequest.Builder 11 (Continued) |
|---|
| - HttpRequest.Builder GET()<br>- HttpRequest.Builder DELETE()<br>- HttpRequest.Builder POST(HttpRequest.BodyPublisher bodyPublisher)<br>- HttpRequest.Builder PUT(HttpRequest.BodyPublisher bodyPublisher)<br>sets the request method and body for this request. |

| java.net.HttpResponse<T> 11 |
|---|
| - T body()<br>yields the body of this response.<br>- int statusCode()<br>yields the status code for this response.<br>- HttpHeaders headers()<br>yields the response headers. |

| java.net.HttpHeaders 11 |
|---|
| - Map<String,List<String>> map()<br>yields a Map of these headers.<br>- Optional<String> firstValue(String name)<br>the first value with the given name in these headers, if present. |

# ## 4.5 Sending E-Mail

In the past, it was simple to write a program that sends e-mail by making a socket connection to port 25, the SMTP port, of a mail server. The Simple Mail Transport Protocol (SMTP) describes the format for e-mail messages. Once you are connected to the server, send a mail header (in the SMTP format, which is easy to generate), followed by the mail message.

Here are the details:

+   1. Open a socket to your host.

```
```
var s = new Socket("mail.yourserver.com", 25); // 25 is SMTP
var out = new PrintWriter(s.getOutputStream(), StandardCharsets.UTF_8);
```
```