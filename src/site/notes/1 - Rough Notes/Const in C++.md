---
{"dg-publish":true,"permalink":"/1-rough-notes/const-in-c/"}
---

# `Const` in C++

27-07-2024 01:22

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]]

- All const variables must be initialized at time of creation.
```cpp
const int x;      // compile error: not initialized
const int y{};    // ok: value initialized
const int z{ 5 }; // ok: list initialized
```
- `const` pointer
```cpp
const int* pp; // cannot change the contents of the pointer
int const* pp; // same thing. const should be before the pointer

int* const pp; // cannot change the pointer. const if after change the pointer
```
- `const` in class
```cpp
// const in method inside classes. will only work with class methods and not other functions
class Tempo{
public:
	int m_x, m_y;

	void getVar() const // cannot modify class variables. A read only method
	{
	}

}
``` 
- below will work if `getVar` is const method  but will not work if `getVar` is not constant method because we are passing const reference to the `func`. a non-const `getVar` does not guarantee that it will leave the value unchanged. Therefore sometimes people define two version of the method. One with `const` and one without.
```cpp
class Tempo{
public:
	int m_x, m_y;

	void getVar() const // cannot modify class variables. A read only method
	{
	}

	void getChar()
	{
	}
}

void func1(const Tempo& t){
 cout << t.getVar(); // will work
}

void func2(const Tempo& t){
 cout << t.getChar(); // will not work
}
``` 
- if you still want to modify a variable inside a `const` method for some reason, define it as `mutable`. It allows functions/methods which are `const` to modify the variable. (maybe use for debugging purposes??)
```cpp
class Tempo{
public:
	int m_x, m_y;
	mutable int x;
	
	void getVar() const // cannot modify class variables. A read only method
	{
	 x = 111; // will work
	}
}
```


## References
- The Cherno - YouTube
- [LearnCPP](https://www.learncpp.com)