---
{"dg-publish":true,"permalink":"/1-rough-notes/static-in-c/"}
---

# `Static` in $C++$

27-07-2024 01:27

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]]

## Static Local Variables 
- Global variables have `static duration`, which means they are created when the program starts and destroyed when the program ends.
- Any static variables are created when the program starts and destroyed at the end of the program
- Using the `static` keyword on a local variable changes its duration from `automatic duration` to `static duration`. This means the variable is now created at the start of the program, and destroyed at the end of the program (just like a global variable)
```cpp
#include <iostream>

void incrementAndPrint()
{
    static int s_value{ 1 }; // static duration via static keyword.  This initializer is only executed once.
    ++s_value;
    std::cout << s_value << '\n';
} // s_value is not destroyed here, but becomes inaccessible because it goes out of scope

int main()
{
    incrementAndPrint();
    incrementAndPrint();
    incrementAndPrint();

    return 0;
}
```

```bash TITLE=OUTPUT
# output
2
3
4
```

> [!note] Key insight
> - A static local variable has block scope like a local variable, but its lifetime is until the end of the program like a global variable.
> - Static local variables can be used when a function needs a persistent object that is not directly accessible outside of the function.

## Initialization of Static Variables
Initialization of static variables happens in two consecutive stages: _static_ and _dynamic_ initialization.

Static initialization happens first and usually at compile time. If possible, initial values for static variables are evaluated during compilation and burned into the ==data section of the executable==. Zero runtime overhead, early problem diagnosis, and, as we will see later, safe. This is called [constant initialization](https://en.cppreference.com/w/cpp/language/constant_initialization). In an ideal world all static variables are const-initialized.

If the initial value of a static variable can’t be evaluated at compile time, the compiler will perform zero-initialization. Hence, during static initialization all static variables are either const-initialized or zero-initialized.

```cpp
#include <iostream>

void incrementAndPrint()
{
    static int s_value; // no initial value
    ++s_value;
    std::cout << s_value << '\n';
}

int main()
{
    incrementAndPrint();
    incrementAndPrint();
    incrementAndPrint();

    return 0;
}
```
OUTPUT
```js
1
2
3
```

After static initialization, dynamic initialization takes place. Dynamic initialization happens at runtime for variables that can’t be evaluated at compile time. Here, static variables are initialized every time the executable is run and not just once during compilation.

## Static in Classes and Structs in $C++$

- A static variable in a class is like a global variable for that class
```cpp
class Entity{
public: 
	static int common = 100;
};
```
- Why not make a global variable? Well, because of organizational purposes. Say you had 100 classes and each of them had like 3/4 static member variables. It would be very hard to keep track of them and manage them.
- If you create a static variable in a class but do not initialize and you do not use it **ANYWHERE** in the code, there would not be any errors (at compile time as well as runtime) **BUT** if you use it anywhere without initialization, there will be error at compile time itself. Thus, you need to initialize it first like this 
```cpp
class Entity{
public: 
	static int common = 100;
};

int Entity::common;
```
- If you create same static variable once in say, the parent class and somewhere down the line in a child class (with the same name and type), they will be different. 
```cpp
class A{
public:
	static int x;
}

class B: A{
public:
	static int x;
}

// both are different. The static in B hides the static in A. Will have to deal with both of them differently
```
- to access a static member of a class, you use `ClassName::staticVariableName`
```cpp
A::x;
```
> [!caution]
> Static members cannot be inherited because they belong to the class declaring them (because they are actually just global variables with some more advanced access), but your derived class can still access them without having to write `Base::` (of course they have to be atleast `protected`). Access also means that you can set them.
```cpp
class A{
public:
	static int x;
}

class B: A{
public:
	B(){
		x++; // completely valid and no need to use A::x
	}
}

A::x; // valid
B::x; // Not valid
```

- static methods cannot access non-static variables because a static method does not have a class instance. unlike non static method, the class instance is not passed as a parameter.
- every non static method that is written always gets an instance of the current class as a parameter
- a static method is like writing a function outside the class so it makes a lot of sense in that way as to why a static method cannot access non static variables.
```cpp
class Entity{
public: 
	static int common = 100;
	int x{};
	
	static void Print() // valid
	{
		cout << "aaaaa" << common << '\n';
	}
	
	static void Print2() // not valid
	{
		cout << "aaaaa" << x << '\n';
	}
};
```
- When a non static method is compiled this is what happens
```cpp
class Entity{
public: 
	static int common = 100;
	int x{};
	void Print()
	{
		cout << x;
	}
};
```
this is what happens at compile time
```cpp

void Print(Entity e)
{
	cout << e.x;
}
```

- Guess the output:
```cpp
#include <iostream>
#include <string>

using namespace std;

class SomeClass
{
    public:
        SomeClass() {total++;}
        static int total;
        void Print(string n) { cout << n << ".total = " << total << endl; }
};

int SomeClass::total = 0;

class SomeDerivedClass: public SomeClass
{
    public:
        SomeDerivedClass() {total++;}
};

int main(int argc, char ** argv)
{
    SomeClass A;
    SomeClass B;
    SomeDerivedClass C;

    A.Print("A");
    B.Print("B");
    C.Print("C");

    return 0;
}
```
OUTPUT:
```cpp
A.total = 4
B.total = 4
C.total = 4
```
All three print statements will output 4. This is because after creating A, total will increment by 1. After creating B, it will increment by 1. After creating C, it will increment by 2 since derived class always invokes constructor of base class. [[1 - Rough Notes/Constructors in C++\|Constructors in C++]]
## References
- https://stackoverflow.com/questions/21223767/how-inherit-static-members
- https://stackoverflow.com/questions/998247/are-static-fields-inherited 
- https://cplusplus.com/forum/general/80589/
- https://pabloariasal.github.io/2020/01/02/static-variable-initialization/