# Accessing Java Strings from C Code

+   - `jstring NewStringUTF(JNIEnv* env, const char bytes[])`
+     returns a new Java string object from a zero byte-terminated “modified UTF-8” byte sequence, or NULL if the string cannot be constructed.
+   - `jsize GetStringUTFLength(JNIEnv* env, jstring string)`
+     returns the number of bytes required for the “modified UTF-8” encoding (not counting the zero byte terminator).
+   - `const jbyte* GetStringUTFChars(JNIEnv* env, jstring string, jboolean* isCopy)`
+     returns a pointer to the “modified UTF-8” encoding of a string, or NULL if the character array cannot be constructed. The pointer is valid until ReleaseStringUTFChars is called. isCopy points to a jboolean filled with JNI_TRUE if a copy is made, or with JNI_FALSE otherwise.
+   - `void ReleaseStringUTFChars(JNIEnv* env, jstring string, const jbyte bytes[])`
+     informs the virtual machine that the native code no longer needs access to the Java string through bytes (a pointer returned by GetStringUTFChars).
+   - `void GetStringRegion(JNIEnv *env, jstring string, jsize start, jsize length, jchar *buffer)`
+     copies a sequence of UTF-16 double bytes from a string to a user-supplied buffer of size at least 2 × length.
+   - `void GetStringUTFRegion(JNIEnv *env, jstring string, jsize start, jsize length, jbyte *buffer)`
+     copies a sequence of “modified UTF-8” bytes from a string to a user-supplied buffer. The buffer must be long enough to hold the bytes. In the worst case, 3 × length bytes are copied.
+   - `jstring NewString(JNIEnv* env, const jchar chars[], jsize length)`
+     returns a new Java string object from a Unicode string, or NULL if the string cannot be constructed.
+   - `jsize GetStringLength(JNIEnv* env, jstring string)`
+     returns the number of characters in the string.
+   - `const jchar* GetStringChars(JNIEnv* env, jstring string, jboolean* isCopy)`
+     returns a pointer to the Unicode encoding of a string, or NULL if the character array cannot be constructed. The pointer is valid until ReleaseStringChars is called. isCopy is either NULL or points to a jboolean filled with JNI_TRUE if a copy is made, or with JNI_FALSE otherwise.
+   - `void ReleaseStringChars(JNIEnv* env, jstring string, const jchar chars[])`
+     informs the virtual machine that the native code no longer needs access to the Java string through chars (a pointer returned by GetStringChars).