# LINUX

Most Linux distributions typically ship with a version of the GNU C compiler [gcc] installed. As of CUDA 3.0, the following Linux distributions shipped with supported versions of gcc installed:

+   - Red Hat Enterprise Linux 4.8
+   - Red Hat Enterprise Linux 5.3
+   - OpenSUSE 11.1
+   - SUSE Linux Enterprise Desktop 11
+   - Ubuntu 9.04
+   - Fedora 10

If you're a die-hard Linux user, you're probably aware that many Linux software packages work on far more than just the "supported" platforms. The CUDA Toolkit is no exception, so even if your favorite distribution is not listed here, it may be worth trying it anyway. The distribution's kernel, gcc, and glibc versions will in a large part determine whether the distribution is compatible.

# MACINTOSH OS X

If you want to develop on Mac OS X, you will need to ensure that your machine has at least version 10.5.7 of Mac OS X. This includes version 10.6, Mac OS X "Snow Leopard." Furthermore, you will need to install gcc by downloading and installing Apple's Xcode. This software is provided free to Apple Developer Connection (ADC) members and can be downloaded from http://developer.apple.com/tools/xcode. The code in this book was developed on Linux and Windows platforms but should work without modification on Mac OS X systems.

# 2.3 Chapter Review

If you have followed the steps in this chapter, you are ready to start developing code in CUDA C. Perhaps you have even played around with some of the NVIDIA GPU Computing SDK code samples you downloaded from NVIDIA's website. If so, we applaud your willingness to tinker! If not, don't worry. Everything you need is right here in this book. Either way, you're probably ready to start writing your first program in CUDA C, so let's get started.