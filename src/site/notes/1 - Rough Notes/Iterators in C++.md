---
{"dg-publish":true,"permalink":"/1-rough-notes/iterators-in-c/"}
---


# Iterators in C++

20-08-2024 22:18

Status: 

Tags: [[3 - Tags/CPP\|CPP]]

## Structured Bindings
- as of C++17, we can do something like 
```cpp
unordered_map<int, int> m;
for(auto [key, value]: m){
	cout << key << "= " << value << '\n';
}
```
- It allows you to bind multiple variables to the elements of a structured object, such as a tuple or struct, in a single declaration. 
- This can make your code more concise and easier to read, especially when working with complex data structures.

## References
- [Structured Bindings](https://www.cppstories.com/2022/structured-bindings/)