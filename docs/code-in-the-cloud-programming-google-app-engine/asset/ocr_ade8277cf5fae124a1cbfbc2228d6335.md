Once you’re sitting in front of the application control panel, you’re just about ready to start programming. Notice, though, that programming for the cloud is different from other kinds of development. You can’t edit files on the Google App Engine server. You need to write them locally and then use an administrative script to transfer them into the App Engine environment, where they can run.

The next step is to get the tools. On your control panel, toward the bottom left, you’ll see a box labeled Resources. This box contains links to software, forums, and documentation that you’ll want as you learn and use Google App Engine. For right now, click on the Download link and download the appropriate version of the App Engine SDK for Python. Once it’s downloaded, go ahead and install it. The installation process varies slightly, depending on which operating system you’re using: for Windows or Macintosh, the download contains an automated installation program—just run it, and it will do the work. If you’re using Linux, the download is a zip file, so unzip it in an appropriate location.

If you’re using Windows or MacOS, you’re all ready to start. If you’re using Linux, take the directory where you unpacked the SDK zip file and add it to your path.

There are two main programs in the SDK that you’ll use:

+   - `dev_appserver.py` runs a simulated Google App Engine environment that you can use to test your applications on your local computer.
+   - `appcfg.py` uploads and configures your applications using Google App Engine in the cloud.

# 2.3  Starting to Program in Python with Google App Engine

Now we’re ready to do some programming!

Python App Engine is, at its core, very simple. The main engine is a lightweight, secure CGI executor. CGI is one of the oldest interfaces for executing programs in response to HTTP requests. The bare bones of Google App Engine are pure CGI. The big advantage of this is that if you’ve ever done any CGI scripting in Python, you can just about take those scripts and use them in Google App Engine. Any framework and any Python library that was written for CGI scripting can be used in Google App Engine—just include the framework/library files when you upload your application code.