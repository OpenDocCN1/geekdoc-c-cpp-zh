# BOX 4 ■ Source Code for Library H3lp’s Widget

```
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<meta http-equiv=content-type content="text/html; charset=UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0 user-scalable=yes" />
<title></title>
<link type="text/css" rel="stylesheet" href="/css/mobile.css" />

<style id="dynamic" type="text/css">
</style>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js"></script>
<script type="text/javascript" src="http://d1aaqh87bn7fin.cloudfront.net/mobile_2010011801.min.js"></script>
<!--
<script type="text/javascript" src="/js/lib/strophe.js"></script>
<script type="text/javascript" src="/emoticons/emoticons.js"></script>
<script type="text/javascript" src="/js/mobile.js"></script>
-->
</head>
<body>
<div id="header">
<img id="presence" src="/presence/image/simpletext/unavailable" />
<h1 id="title"></h1>
</div>

<div id="to" jid="my-queue@chat.libraryh3lp.com" lang="en"></div>
<div id="recv"></div>
<div id="send">
<form action="#" method="post" onSubmit="return false;">
<textarea id="msg">chat requires javascript...</textarea>
</form>
<div id="buttons"><a href="#" onclick="libraryh3lp.sendLine(); return false;"><img height="42" width="30" src="/images/mobilesend.png" /></a></div>
</div>
<div id="status"><a id="mail" href="#" onclick="libraryh3lp.mailTranscript(); return false;">Email transcript</a></div>
</body>
</html>
```