# mmap-payload
Nim program that allocate memory on the heap as executable and execute a payload inside

# compile
You can compile the source code using:  
```
nim c --d:release mmap_payload.nim
```

# result
It should look similar to this:
```
➜ ./mmap_payload 
0x7ff421f62000 = mmap(nil, 57, 6, 34, -1, 0)
Hello, World !
Hello, Nim is Powerful :)
```
- The memory is freed after usage

# payload
The payload in the source code is a simple Hello World in 64bit asm:
```
   0:   55                      push   %rbp
   1:   48 89 e5                mov    %rsp,%rbp
   4:   48 b8 6f 72 6c 64 20    movabs $0xa0a2120646c726f,%rax
   b:   21 0a 0a 
   e:   50                      push   %rax
   f:   48 b8 48 65 6c 6c 6f    movabs $0x57202c6f6c6c6548,%rax
  16:   2c 20 57 
  19:   50                      push   %rax
  1a:   48 c7 c0 01 00 00 00    mov    $0x1,%rax
  21:   48 c7 c7 01 00 00 00    mov    $0x1,%rdi
  28:   48 89 e6                mov    %rsp,%rsi
  2b:   48 c7 c2 0f 00 00 00    mov    $0xf,%rdx
  32:   0f 05                   syscall 
  34:   48 89 ec                mov    %rbp,%rsp
  37:   5d                      pop    %rbp
  38:   c3                      ret
```
