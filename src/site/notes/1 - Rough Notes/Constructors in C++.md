---
{"dg-publish":true,"permalink":"/1-rough-notes/constructors-in-c/"}
---

# Constructors in $C++$

27-07-2024 15:16

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]] 
References: [[1 - Rough Notes/Static in C++\|Static in C++]]

- constructor has no return type, same name as the class name.
```cpp
Foo foo{}; // value initialization, calls Foo() default constructor
Foo foo2;  // default initialization, calls Foo() default constructor
```
- if you create a constructor for a class, the default constructor is no more there. You'll manually need to create a default constructor
```cpp
class Prank{
public:
    Prank(int age, string name){
        cout << "you cannot create class\n";
    }
};

class April {
public:
    
    April(){}

    April(int age, string name, int month){
        cout << "appapapa\n";
    }
};



int main(){
   Prank p2; // will not work since we created our own constructor, the default one got deleted
   April a1; // will work since we also provided a default constructor also
}
```
- fastest way
```cpp
Prank p1 = Prank(1,"asdasd"); // fastest way
```
- if you make a constructor private, you no longer will be able to create the object
- you can have multiple constructors with different parameters just like how you would have function overloads
- if you have a class just with static methods and you don't want users to be able to instantiate an object of the class, you can either `delete` the constructor or make the constructor private
```cpp
class PPP{
public: 
	static void Write()
	{
		cout << "Hola\n";
	}
};

class PPP2{
public: 
	PPP2() = delete;
	static void Write()
	{
		cout << "Hola\n";
	}
};

class PPP3{
private:
	PPP2()
	{
	}
public: 
	static void Write()
	{
		cout << "Hola\n";
	}
};

int main(){

	PPP1 p1; // we don't want this
	PPP::Write(); // we only want this

	PPP2 p2; // wont work since default constructor is destroyed
	PPP3 p3; // wont work since constructor is private
	
	return 0;
}
```
> [!caution]
> In C++, **a derived-class constructor always invokes a constructor for the base class**. If an explicit invocation does not appear in the member-initializer list, there is an implicit call to the default constructor. 
> check out the example [[1 - Rough Notes/Static in C++\|Static in C++]]

## Order of construction of derived classes
- We can think of derived class as a two part class: one part derived, and one part Base.
![Pasted image 20240815154542.png](/img/user/1%20-%20Rough%20Notes/attachments/Pasted%20image%2020240815154542.png)
- Remember that C++ always constructs the “first” or “most base” class first. It then walks through the inheritance tree in order and constructs each successive derived class.
```cpp 
#include <iostream>

class A
{
public:
    A()
    {
        std::cout << "A\n";
    }
};

class B: public A
{
public:
    B()
    {
        std::cout << "B\n";
    }
};

class C: public B
{
public:
    C()
    {
        std::cout << "C\n";
    }
};

class D: public C
{
public:
    D()
    {
        std::cout << "D\n";
    }
};

int main()
{
    std::cout << "Constructing A: \n";
    A a;

    std::cout << "Constructing B: \n";
    B b;

    std::cout << "Constructing C: \n";
    C c;

    std::cout << "Constructing D: \n";
    D d;
}
```
OUTPUT
```cpp
Constructing A:
A
Constructing B:
A
B
Constructing C:
A
B
C
Constructing D:
A
B
C
D
```

## A class should have only one default constructor
If more than one default constructor is provided, the compiler will be unable to disambiguate which should be used. A trick example is
```cpp
#include <iostream>

class Foo
{
private:
    int m_x {};
    int m_y {};

public:
    Foo() // default constructor
    {
        std::cout << "Foo constructed\n";
    }

    Foo(int x=1, int y=2) // default constructor
        : m_x { x }, m_y { y }
    {
        std::cout << "Foo(" << m_x << ", " << m_y << ") constructed\n";
    }
};

int main()
{
    Foo foo{}; // compile error: ambiguous constructor function call

    return 0;
}
```
In the above example, we instantiate `foo` with no arguments, so the compiler will look for a default constructor. It will find two, and be unable to disambiguate which constructor should be used. This will result in a compile error.

















> [!question] When do you need private constructors?
> https://stackoverflow.com/questions/6568486/when-do-we-need-a-private-constructor-in-c

## References