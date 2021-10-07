# LD_PRELOAD-Example
This repository is an example of how LD_PRELOAD works to overload functions using the dynamic linker

## About: 
This example repository is based on the following tutorial: 
https://catonmat.net/simple-ld-preload-tutorial

As you can see, fopen got replaced with our own version that is always failing.

This is really handy if you need to debug or replace certain parts of programs or libraries that you didn't write.

Man page for [ld.so/LD_PRELOAD](https://man7.org/linux/man-pages/man8/ld.so.8.html)

## Steps: 
```
$ ls
prog.c  test.txt
```
```
$ gcc prog.c -o prog
```
```
$ ls
prog  prog.c  test.txt
```
```
$ ./prog
Calling the fopen() function...
fopen() succeeded

```
Let's compile it as a shared library called myfopen.so:


```

gcc -Wall -fPIC -shared -o myfopen.so myfopen.c
```
```
$ LD_PRELOAD=./myfopen.so ./prog
Calling the fopen() function...
Always failing fopen
fopen() returned NULL
```