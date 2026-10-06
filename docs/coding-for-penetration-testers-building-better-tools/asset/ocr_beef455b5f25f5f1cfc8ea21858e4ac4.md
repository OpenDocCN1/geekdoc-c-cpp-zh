root@mostdefinitelynotcall: ~/Desktop

```
root@mostdefinitelynotcall:~/Desktop# perl -MLWP -e "getprint 'http://ww
www.com"
<!DOCTYPE TYPE><html>html class="no-js"><meta content="ie=edge,chrome=1"> http-o
<meta name="UA-Compatible"><meta charset="utf-8"><meta content="text/html" http-o
-type="Content-Type">\meta name="viewport" content="width=device-width, initial-sc
e=1.0, minimum-scale=1.0"><link rel="icon" href="http://i.cdn.cnn.com/favicon.io" rel="Short Icon" type="image/x-icon"><link href="http://i.cdn.cnn.com/img/3.0/global/msc/
apple-touch-icon.png" rel="apple-touch-icon" type="image/png"><script var CNN
N |"><meta name="pagetimer" content="interval:28,isvisible="true,page="section"
<meta name="description" content="Breaking News, World and Videos - CNN.com;title content="homepage-page
aking News, with the News and Videos - CNN.com;title content="homepage-page
-meta name="section" content="2014-02-09T19:15:02" property="og:published" content="00:03:32
-2014-02-09T19:15:02" property="og:published" content="12:13:00:32 n
 name="last"><meta content="http://www.cnn.com" property="og:title" meta
entent-Breaking News, World and Videos - CNN.com."property="og:description" meta con
tainment, politics and health at CNN.com." content="The latest breaking news for US., world, weather, enter
tainment, politics and health at CNN.com."meta name="description" meta content-
n, daily news, breaking news, news today, current events" name="keywords">-
meta content="og:site name="meta content="summary_large_images" n
canonical" content="http://www.cnn.com"meta content="8040132489" property="f
b:app_id" rel="canonical" content="http://www.cnn.com"><link rel="publisher"
```

# FIGURE 8.2 LWP:Simple output.

All we did was invoke the LWP interpreter, tell it to use the
LWP::Simple module, and tell it to get and print the URL specified.
That was pretty simple, right?
We ended up with a fairly raw version of the Web page, but this is just
 fine if we're planning to do it with something simple, such as
parsing strings out of the page. As we said, we can approach this
in several ways, and we can get out of the end of the feature
sspectrum with the WWW::Mechanize module.

# WWW ::Mechanize

The WWW::Mechanize module is a great and (potentially) costly benefit.
We can do anything nearly from WWW::Mechanize that we can do from a
Web browser with a person operating. Follow links, download and upload files, run searches, and
great deal more. The nice thing that WWW::Mechanize is that we can
still do things in a relatively simple fashion if the task we need