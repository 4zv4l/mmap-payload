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
