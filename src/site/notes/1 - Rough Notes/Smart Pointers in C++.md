---
{"dg-publish":true,"permalink":"/1-rough-notes/smart-pointers-in-c/"}
---


# Smart Pointers in C++

21-08-2024 08:14

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]]

## Weak pointers

- copying a shared pointer to a weak pointer won't increase the reference count.
- typically used when one doesn't want ownership of the object.

## How to create smart pointers
### Unique pointers
- int the header file `<memory>`
- You can do it two ways
```cpp

	std::unique_ptr<A> entity(new A()); // will work
	std::unique_ptr<A> entity = std::make_unique<A>(); // safer due to exception safety

	std::unique_ptr<A> entity = new A(); // wrong. The constructor needs to be explicit
```
The second way is much safer because it deals with exception safety. If our constructor throws some exception, the first method might give us a dangling pointer but second method will deal with it.
- The copy constructor and copy assignment operators are deleted (check the implementation). That is what stops us from creating a copy of the `unique_ptr`.
## References