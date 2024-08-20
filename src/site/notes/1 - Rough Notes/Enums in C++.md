---
{"dg-publish":true,"permalink":"/1-rough-notes/enums-in-c/"}
---

# Enums in $C++$

27-07-2024 15:02

Status: 

Tags: [[3 - Tags/CPP\|CPP]]

- Enums is short for enumeration
- enums are basically integers
- it is a way to give a name to a value
- helps in define a set of value
- restricts what values we can assign to them
- makes code more readable and organized

```cpp
// not grouped
int monday = 0;
int tuesday = 1;
int wednesday = 2;
int thursday = 3;

// can suddeny introduce new values later
int friday = 4;
int saturday = 5;
```
- Do this instead
```cpp
enum Days{
	mon, tue, wed, thur, fri, sat
	// first value is set to 0. rest increment by one
};

enum Example{
	oo = 1, oooo, ooooo
	// rest values are 2 and 3 respectively
};

Days d = 1; // wrong
Days d = mon; // correct
```
- we can define what type of integer we want the enum to be
```cpp
enum Example: unsigned char
{
	A, B, C
};
```
- enums are not really namespace
- a common practice for enums
```cpp
// prefix the name with the enum name
enum Example{
	ExampleA, ExampleB, ExampleC
};
```
## References