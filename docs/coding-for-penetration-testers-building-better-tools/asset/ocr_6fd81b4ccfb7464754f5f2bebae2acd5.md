![](bbox=[0.117, 0.095, 0.863, 0.489])

FIGURE 1.8 Output from looping2.sh.

# Putting It All Together With Bash

Now we'll put together a quick port scanner using bash. The core of our scanner will be the /dev/tcp device, which will enable us to utilize the built-in networking functionality of which bash is capable. Depending on the particular platform on which we are running bash, support for /dev/tcp may not be built into the version of bash we are running, we can generally fix that. In particular, many distributions related to Debian may have this issue, including the Kali 2.0 distribution we are using for our examples in this chapter. We can check for /dev/tcp support by running step 5 in the following section.

> Root access will be needed to carry out most of what we will be discussing in this section. Within the Kali environment, this should not be an issue, but in other cases logging in or su-ing to