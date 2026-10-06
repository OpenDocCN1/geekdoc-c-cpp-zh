```
FunctionA();
FunctionB();
```

Now, we can rearrange these snippets to a form that is much more complicated (in assembly):

```
main:
  jmp FAP1
  FBP3: call FuncBP3
  jmp end
  FBP1: call FuncBP1
  jmp FBP2
  FAP2: call FuncAP2
  jmp FAP5
  FBP2: call FuncBP2
  jmp FBP3
  FAP1: call FuncAP1
  jmp FAP2
  FAP3: call FuncAP3
  jmp FBP1
end:
```

As you can see, this is much harder to read, although it perfectly preserves the program flow of the original code. This code is much harder for a human to read, although it isn\u20t hard at all for an automated debugging tool (such as IDA Pro) to read.

# 25.7 Opaque Predicate

An Opaque Predicate is a predicate inside the code, that cannot be evaluated during static analysis. This forces the attacker to perform a dynamic analysis to understand the result of the type. Typically this is related to a branch instruction that is used to prevent in static analysis the understanding which code path is taken.

# 25.8 Code Encryption

Code can be encrypted, just like any other type of data, except that code can also work to encrypt and decrypt itself. Encrypted programs cannot be directly disassembled. However, such a program can also not be run directly because the encrypted opcodes cannot be interpreted properly by the CPU. For this reason, an encrypted program must contain some method for decrypting itself prior to operation.

The most basic method is to include a small stub program that decrypts the remainder of the executable, and then passes control to the decrypted routines.

# 25.8.1 Disassembling Encrypted Code

To disassemble an encrypted executable, you must first determine how the code is being decrypted. Code can be decrypted in one of two primary ways: