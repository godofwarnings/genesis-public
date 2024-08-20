---
{"dg-publish":true,"permalink":"/1-rough-notes/how-c-works/"}
---

# How C++ works

30-07-2024 23:23

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/COMPILER\|COMPILER]]

### Preprocessor Statements
- any line beginning with a $\#$ is a pre-processor statement. The first thing the compiler does is preprocesses these statements
- header files are literally copy and pasted.
### int main()
- entry point for the application. When we start running our code, this is where the application starts running
- code is executed line by line 
- by default returns 0 (i.e. if not written in the end). It is a special case. In all other functions, you will have to specify

### Compiler
- during compilation, we can specify the platform we want it to run on.
- we can specify if we want to compile it as an application executable (.exe) or libraries (dynamic library .dll or static library .lib)
- In general, debug mode is slower because the compiler does not do any optimization
- header files first get included into our cpp file then the cpp file is compiled

- cpp files first get converted to object files.
- these object files are then stitched together through a linker into a single executable
- when compiling an individual file, no linking happens (obviously)

- when compiling a single file, we just need the function declaration and the compiler believes us. It thinks that we will provide it with the function. Since the function definition is in another file, it is now the linker's job to find the location function.
```cpp nums main.cpp
// main.cpp
#include <iostream>

void Log(const char* message);

int main(){
	Log("This will compile without a hitch");
}
```



### Linker
- its job is to resolve symbols
- unresolved external symbol: if we were to compile the whole project, i.e. the main.cpp and the file containing the function definition, and have the wrong function, say it is called `Logr` instead of `Log`, the linker will give this error, meaning it did not find the right "symbol" which is the function in our case.

## References

- [The Cherno $C++$](https://youtube.com/playlist?list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb&si=sJU1xEyupin8VQKO)
- CSAPP : pg 41-43 ![[Computer Systems A Programmer’s Perspective-Pearson (2016).pdf]]