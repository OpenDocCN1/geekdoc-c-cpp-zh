# **Listing 12.20** `invocation/InvocationTest.c`

```
```c
/**
 * @version 1.20 2007-10-26
 * @author Cay Horstmann
 */

#include <jni.h>
#include <stdlib.h>

#ifdef _WINDOWS

#include <windows.h>
static HINSTANCE loadJVMLibrary(void);
typedef jint (JNICALL *CreateJavaVM_t)(JavaVM **, void **, JavaVMInitArgs *);

#endif

int main()
{
    JavaVMOption options[2];
    JavaVMInitArgs vm_args;
    JavaVM *jvm;
    JNIEnv *env;
    long status;

    jclass class_Welcome;
    jclass class_String;
    jobjectArray args;
    jmethodID id_main;

#ifdef _WINDOWS
    HINSTANCE hjvmlib;
    CreateJavaVM_t CreateJavaVM;
#endif

    options[0].optionString = "-Djava.class.path=.";

    memset(vm_args, 0, sizeof(vm_args));
    vm_args.version = JNI_VERSION_1_2;
    vm_args.nOptions = 1;
    vm_args.options = options;

#ifdef _WINDOWS
    hjvmlib = loadJVMLibrary();
    CreateJavaVM = (CreateJavaVM_t) GetProcAddress(hjvmlib, "JNI_CreateJavaVM");
    status = (*CreateJavaVM)(&jvm, (void **) &env, &vm_args);
```
```

*Continues*