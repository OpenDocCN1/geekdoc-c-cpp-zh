typos or other compile errors would be caught and their cause reported. Calls to checkOpenGLError() could be added after runtime OpenGL calls, such as immediately after the call to glDrawArrays().

Another reason that it is important to use these tools is that *a GLSL error does not cause the C++ program to stop.* So unless the programmer takes steps to catch errors at the point that they happen, debugging will be very difficult.

# Program 2.3 Modules to Catch GLSL Errors

```
void printShaderLog(GLuint shader) {
    int len = 0;
    int chWritten = 0;
    char *log;
    glGetShaderiv(shader, GL_INFO_LOG_LENGTH, &len);
    if (len > 0) {
        log = (char *)malloc(len);
        glGetShaderInfoLog(shader, len, &chWritten, log);
        cout << "Shader Info Log: " << log << endl;
        free(log);
    }
}

void printProgramLog(int prog) {
    int len = 0;
    int chWritten = 0;
    char *log;
    glGetProgramiv(prog, GL_INFO_LOG_LENGTH, &len);
    if (len > 0) {
        log = (char *)malloc(len);
        glGetProgramInfoLog(prog, len, &chWritten, log);
        cout << "Program Info Log: " << log << endl;
        free(log);
    }
}

bool checkOpenGLError() {
    bool foundError = false;
    int glErr = glGetError();
    while (glErr != GL_NO_ERROR) {
        cout << "glError: " << glErr << endl;
        foundError = true;
        glErr = glGetError();
    }
    return foundError;
}
```