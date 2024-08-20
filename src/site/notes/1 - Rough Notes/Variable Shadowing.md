---
{"dg-publish":true,"permalink":"/1-rough-notes/variable-shadowing/"}
---

# Variable Shadowing

11-06-2024 22:37

Status: 

Tags: [[3 - Tags/CPP\|CPP]]

## Learning

- If you declare multiple variables with same name in different scopes, the inner most scope is considered. For example
```cpp

int a = 4;

{
	cout << a;
	int a = 5;
	cout << a;
}

cout << a;
```
would output
```bash
4
5
4
```
- Similarly, if you have a global and a local variable, then doing any modification to the variable where local variable is also in scope will modify the local variable and not the global variable.



## References

- https://www.learncpp.com/cpp-tutorial/variable-shadowing-name-hiding/