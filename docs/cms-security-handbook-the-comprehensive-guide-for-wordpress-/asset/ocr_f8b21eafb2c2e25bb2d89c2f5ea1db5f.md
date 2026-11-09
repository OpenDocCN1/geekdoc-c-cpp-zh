+   - Mediawiki
+   - Moodle
+   - MovableType
+   - osCommerce
+   - phpBB
+   - phpMyAdmin
+   - phpNuke
+   - SPIP
+   - WordPress

In addition, it reveals more than a dozen plugins for Drupal and two dozen for WordPress. The obvious implication for this is easy identification of your CMS.

Next, the hacker needs the web server version. Given Apache is by and large the most popular web server out there, a likely chance exists that the site is being run under Apache. But the attacker must verify that is the case, and identify the version.

One quick method to do this is to send the web server a request for a bogus page. The attacker could type in a non-existent web page at a site to see what error results. For example, suppose that, at the browser, the attacker entered the following for a political website:

```
http://www.domain.com/candidates.html
```

The hacker would then receive back from the server the error message shown in Figure 1-2.

![](bbox=[0.135, 0.649, 0.627, 0.752])

**Figure 1-2:** Error showing web server version

From the web server’s point of view, the request made is not a huge deal, and it’s certainly a valid request. The browser asked for the candidates.html page, and because it didn’t exist, the server could not produce the page. It gave the default error of Not Found and the other information.

Notice that the hacker was not directed to a “404 page” offering other information — for example, another page that may contain helpful information such as links on the site. The web server did not even send the attacker to a page explaining that the information requested does not exist.