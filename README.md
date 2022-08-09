# Extending c with python (Write your own C Modules).

#### Tip: Make sure you have searched python for the module before writing one. Because there are already alot of Modules already available, ready to use, in Python.

# 1- Ctypes : 
**ctypes** is a foreign function library for Python. It provides C compatible data types, 
and allows calling functions in DLLs or shared libraries. It can be used to wrap these libraries in pure Python.


More about Ctypes : <a href="https://docs.python.org/3/library/ctypes.html"> Link </a>

What you will learn :
- Creating a C file (.c extension)
- Creating a shared library file (.so extension) using the GCC compiler.
- Create a ctypes.CDLL instance from the shared file (.so).
- Last, Call the function CDLL_instance.function_name(argument)

**1- Write your C code in a file <YouModule.c> :** \
&emsp;i'm giving an example of simple fibonacci Series
```
#include <stdio.h>

int fiboSeries(int n)
{
    if (n < 2)
        return n;
    else
        return fiboSeries(n-1) + fiboSeries(n-2);
}

```
**2- Open terminal in same <working directory> :** \
 &emsp;Open CMD in same directory where <fiboSeries.c> is present, and then execute : 
  ```
  gcc -shared -Wl,-soname,fiboSeries -o fiboSeries.so -fPIC fiboSeries.c
  ```
  
**3- Now create a wrapper :** \
&emsp;_All you need is the Shared Object File .so (Shared Library)_
```
import ctypes

fibo2 = ctypes.CDLL("fibo2lib.so")
print("Fibonacci Series 40 : ",fibo2.fiboSeries(40))
```
Here are some tests i did, In order to check the execution time.

![1](https://user-images.githubusercontent.com/45902447/183598174-84b32c75-79dc-4bae-a37c-a52f9fc75c76.png)

![2](https://user-images.githubusercontent.com/45902447/183598246-97099e20-fc9e-4a26-9b9e-c12e6b6549d0.png)
  
![3](https://user-images.githubusercontent.com/45902447/183598342-10f42994-d63f-4e4e-b125-f5ececdd8c23.png)

  And, Python on google Colab.
 ```
Fibonacci Series 40 :  102334155
Python : 43.03836443399996 seconds
  ```

  
#### That's it this is how easily you can use C functions in Python, Feel free to ask, If you need any help
