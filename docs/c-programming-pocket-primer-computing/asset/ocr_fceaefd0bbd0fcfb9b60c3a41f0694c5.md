```
```c
#include <stdio.h>

int main(int argc, char **argv)
{
   char *pathvar;

   pathvar = getenv("PATH");
   printf("pathvar=%s",pathvar);
}
```
```

Listing 7.14 is straightforward: the `main()` function contains the built-in C function `getenv()` that is involved with the string `PATH`. The result of invoking `getenv()` is the value of the `PATH` environment variable, which is assigned to the character pointer `pathvar`. The last line of code in the `main()` function is the `printf()` function that displays the value of the `PATH` environment variable. The output from compiling and executing the code in Listing 7.14 is here:

```
```text
pathvar=/Users/ocampesato/jython2.5.2:/Users/ocampesato/anaconda/bin:/
opt/local/bin:/Users/ocampesato/android-sdk-mac_86/platform-
tools:/Users/ocampesato/android-sdk-
mac_86/tools:/Users/ocampesato/apache-maven-
3.1.1/bin:/usr/local/bin:/Users/ocampesato/xalan-
j_2.7.1:/Users/ocampesato/lua-
5.1.4/src:/Users/ocampesato/.rvm/bin:/Users/ocampesato/mongoose:/Users/
ocampesato/android-ndk-
r4b:/usr/local/bin:/usr/local/sbin:/usr/local/mysql/bin:/Applications/XAMPP/xa
mppfiles/bin:/Users/ocampesato/phantomjs/bin:../Users/ocampesato/anaconda/bin:/Library/Frameworks/Python.framework/Versions/3.3/bin:/opt/local/bi
n:/opt/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/local/CrossPac
k-
AVR/bin:/usr/local/git/bin:/Users/ocampesato/.rvm/bin:/Users/ocampesato/gr
adle-
1.9/bin:/usr/local/go/bin:/Applications/Xcode.app/Contents/Developer/Toolch
ains/XcodeDefault.xctoolchain/usr/bin:/Users/ocampesato/gyp-read-
only:/Users/ocampesato/depot_tools:/Users/ocampesato/hadoop-
1.1.0/bin:/Users/ocampesato/local/bin:/Users/ocampesato/PebbleSDK-2.0-
BETA5/binoswald-campesatos-macbook:manuscript
```
```