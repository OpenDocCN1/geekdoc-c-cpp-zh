# Chapter 11: Cookies, Ajax, and Security 337

# The Plug-in

```
function FrameBust(message) {
  if (top != self) {
    if (message) {
      if (confirm(message)) {
        top.location.replace(self.location.href)
      }
    } else top.location.replace(self.location.href)
  }
}
```

# ProtectEmail()

Spming these days is worse than ever now the spammers have access to huge botnets of hacked computers and use automated programs to continuously crawl the web looking for e-mail addresses to harvest. However, e-mail is still extremely important and you usually need to display your e-mail address prominently on your site.

Thankfully, with this plug-in you can display your e-mail address in such a way that your users can click or copy it, it will be obfuscated from automatic e-mail harvesters, as shown in Figure 11-6, where the e-mail address is both copyable and clickable but doesn't actually appear as a whole in the web page.

# About the Plug-in

This plug-in obfuscates an e-mail address in such a way that span harvesting programs should not be able to find it. It requires as many arguments as you like because you break your e-mail address into multiple strings and then pass them all as parameters.

# Variables, Arrays, and Functions

| j | Local variable used to iterate through the arguments array |
| a | Local variable containing the e-mail address to display |
| arguments | Array containing all the arguments passed to function |

> Figure 11-6
Use this plug-in to keep your e-mail address visible but unharvestable.

![](bbox=[0.285, 0.772, 0.838, 0.915])