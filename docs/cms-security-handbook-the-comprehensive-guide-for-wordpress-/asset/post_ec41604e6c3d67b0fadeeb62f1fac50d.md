
- **%l** — This field commonly represents the RFC 1413 identity of the client, which is determined by `identd` on the client’s machine.

> **NOTE** Because this information is seldom reliable, the Apache log seldom includes it unless you've made a special configuration. If the information is not available, the field is populated with a hyphen. Thus, when you see a hyphen in the log entry, it means that the information requested is not available.

- **%u** — This field shows the username if the login shows a `userID` of the person requesting the page (which, of course, requires a logged-in user). However, for the most part, you'll likely see another hyphen in this field.

- **%t** — This field indicates the date and time, as shown here:

```text
[17/Sep/2010:08:10:00 -0600]
```

The format is as follows:

```text
[day/month/year:hour:minute:second zone]
day = 2*digit
month = 3*letter
year = 4*digit
hour = 2*digit
minute = 2*digit
second = 2*digit
zone = ('+' | '-') 4*digit
```

- **%r** — This particular field in the log entry is very important. It gives you an idea as to what visitors are requesting from your site. Following is an example of information shown in this field:

```text
"GET /filename.gif HTTP/1.0"
```

The information inside the double quotation marks is the client’s request. This says that the client is using `GET` to connect to the website, and states that the client (the browser or the bot) is requesting the `filename.gif` file. It is using the `HTTP/1.0` protocol.

- **%s** — This field shows a status code. For example, the entry 200 means that all is well. The server sends back a status code to the client to indicate what has happened. You will learn more about the specifics of status codes later in this chapter.

- **%b** — The last part of the log entry, `%b`, indicates the size of the object returned to the client, not including the response headers. As mentioned, if no content was returned to the client, this value will be represented by a hyphen (`-`).

Following is an example of a log entry from an Apache server:

```text
192.168.1.126 - - [09/Sep/2010:12:07:38 -0500]
"GET /components/com_ezautos/ezautos/truck.jpg HTTP/1.1" 200 9643 "http://domain.com/" "Windows; U; Windows NT 5.1; en-US; rv:1.9.1.11) Gecko/20100701 Firefox/3.5.11 (.NET CLR 3.5.*)"
```

Table 8-1 highlights some key areas found in the common log entry format and appearing in this example log entry.

**Table 8-1: Apache Log Format Example**

| VALUE | DEFINITION |
|---|---|
| `192.168.1.126` | This is the IP address from where the visitor originated. |
| `-` | This entry is more or less deprecated. You will almost always see it as a blank. It will be represented by a hyphen in your log entry. |
| `-` | This entry can be the *remote login* name in some cases. Most of the time, it will be blank, and will be represented by a hyphen in the log entry. |
| `09/Sep/2010:12:07:38 -0500` | This is the time and date of the request. This server is in the -0500 time zone, which means that it is five hours away from the Greenwich Mean Time (GMT). In simple terms, that’s Eastern Standard Time (EST) in the U.S. |
| `GET /components/com_ezautos/ezautos/truck.jpg HTTP/1.1` | This entry represents the resource (files, programs, and so on) that the visitor requested. In this example, the resource is the EZ-Autos program, and the visitor has viewed a truck for sale. The HTTP/1.1 entry means that the protocol used to connect is HTTP 1.1. |
| `200` | This is the status code of the entry. |
| `9643` | This is the amount of data transferred, represented in bytes. |

## Combined Log Format

If you look closely at the original example log entry, you’ll notice more data than what Table 8-1 describes. This is because the example entry was actually in a combined log format, which is the preferred format, because of the greater amount of information provided.

With the combined log format, you get the benefit of additional information such as including the Referer (and, yes, that's the way it is spelled). As shown in the following example, this HTTP request header gives the site the visitor came from (that is, it represents the source website):

`http://domain.com/`

Following is another piece of information to note in the earlier example:

```text
(Windows; U; Windows NT 5.1; en-US; rv:1.9.1.11) Gecko/20100701
Firefox/3.5.11 (.NET CLR 3.5.30729)"
```

This provides a boatload of identifying information from the browser, such as its version, brand of browser, and the operating system. This information can be very handy for troubleshooting browser incompatibility. In the example, you can see that the user has a Windows XP or higher machine, running Firefox 3.5.11.

## Status Codes

Any time a web server serves up a request, it marks that request with a code to indicate what happened to that specific request. This is known as a status code. Status codes fall into five major classes and sub-classes. The major classes are all specific to certain classes of activities.

### Apache Status Codes

Table 8-2 can help you quickly read through your Apache logs and identify any issues you may be experiencing.

**Table 8-2: Apache Web Server (httpd) Status Codes**

| CLASS/SUBCLASS | DEFINITION |
|---|---|
| **100 Series** | Informational messages instructing the client that the server has received the information and is continuing to service the request |
| 101 | Continue |
| 102 | Switching protocols |
| **200 Series** | Success — all is well (meaning that the request was accepted and completed) |
| 201 | OK |
| 202 | Created (resource, file, directory, and so on) |
| 203 | Accepted |
| 204 | No content |
| 205 | Reset content |
| 206 | Partial content |
| **300 Series** | Redirection information, meaning that the client (browser and user) must take additional steps to continue |
| 301 | Multiple choices |
| 302 | Moved permanently |
| 303 | See other |
| 304 | Not modified |
| 305 | Use proxy |
| 306 | Not in use |
| 307 | Temporary redirect |
| **400 Series** | Client errors, meaning that something in the request was formatted incorrectly, or was wrong (for example, bad links, attempts to do unauthorized or malicious activities, and so on) |
| 401 | Unauthorized/authorization required |
| 402 | Payment required |
| 403 | Forbidden |
| 404 | Page (resource) not found |
| 405 | Method not allowed |
| 406 | Not acceptable |
| 407 | Proxy authentication required |
| 408 | Request timeout |
| 409 | Conflict |
| 410 | Gone |
| 411 | Length required |
| 412 | Precondition failed |
| 413 | Request entity too large |
| 414 | Requested URI too long |
| 415 | Unsupported media type |
| **500 Series** | Server errors |
| 501 | Internal server errors |
| 502 | Method not implemented |
| 503 | Bad gateway |
| 504 | Service temporarily unavailable |
| 505 | HTTP version not supported |

> **NOTE** For a complete and detailed list of status codes, see http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html.

## Error Logs

By far, error logs are your most important source for spotting trouble. The error log is where your web server will send all information such as diagnostic messages and error messages. If you’re troubleshooting your server, this is the prime location to review for problems. The error log usually provides detailed information about the error and where the error is occurring.

If you’re configuring a brand-new server, then reviewing the error logs will help you through any start-up errors. If a site is hacked, you might see the error log file filling up quickly with PHP or application errors. Reviewing those errors will lead you to the source of trouble in most cases.

The name and location of the error log file is set in the Apache configuration in the ErrorLog Directive. When running a Linux system, the name is typically error_log. This can vary by the distribution of Linux, but identifying it shouldn’t be difficult.

Error logs are broken down into four parts as follows:

```text
[Date] [Severity of error] [IP Address of client] [error message]
```

Following is an example:

```text
[02-Sep-2010 21:27:01] PHP Warning: PHP Startup: Unable to load dynamic
library '/usr/local/lib/php/extensions/no-debug-non-zts-20090626/
pdo_sqlite.so' - /usr/local/lib/php/extensions/no-debug-non-zts-20090626
/pdo_sqlite.so: undefined symbol: sqlite3_libversion in Unknown on line 0
```

This error indicates an issue with the pdo_sqlite.so service.

## Access Logs

Access logs are highly useful for marketing, security, and general knowledge about your site. Access logs are typically located (by default) at /usr/local/apache/domlogs. (However, your location may vary.) If you take a look at that directory, you should see something like what is shown in Figure 8-1.
