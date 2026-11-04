# 8. <SETJMP.H> 73

Introduction 73

Library Variables 73

Library Macros 73

int setjmp(jmp_buf environment) 73

Library Functions 75

void longjmp(jmp_buf environment, int value) 75

# 9. <SIGNAL.H> 77

Introduction 77

Library Variables 77

Library Macros 77

Library Functions 78

void (*signal(int sig, void (*func)(int))) (int) 78

int raise(int sig) 81

# 10. <STDARG.H> 84

Introduction 84

Library Variables 84

Library Macros 84

void va_start(va_list ap, last_arg) 85

type va_arg(va_list ap, type) 86

void va_end(va_list ap) 88

# 11. <STDDEF.H> 90

Introduction 90

Library Variables 90

Library Macros 90

NULL 91

offsetof(type, member-designator) 92

# 12. <STDIO.H> 95

Introduction 95

Library Variables 95