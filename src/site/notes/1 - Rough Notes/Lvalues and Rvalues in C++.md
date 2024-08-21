---
{"dg-publish":true,"permalink":"/1-rough-notes/lvalues-and-rvalues-in-c/"}
---



# `Lvalues` and `Rvalues` in C++

20-08-2024 22:29

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[1 - Rough Notes/Const in C++\|Const in C++]] [[1 - Rough Notes/References in C++\|References in C++]]

## `lvalue` reference to `rvalue`

- C++ allows you to bind a temporary object to a `const` reference. When you do this, the lifetime of the temporary is extended to the lifetime of the reference.
- Something like `int& x = 10` is not valid but something like `const int& x = 10` is valid.
- This feature is commonly used in functions to accept large objects by reference without copying them while still being able to bind to temporary objects
```cpp
void printValue(const int& value) {
    std::cout << value << std::endl;
}

int main() {
	int x = 10;
	printValue(x); // Works
    printValue(10); // Works because a temporary can bind to a const reference
    return 0;
}
```

## How to check for `lvalues` and `rvalues`
### 1. Checking for `lvalues`
- Just make a function with an `lvalue` reference as an input and try and pass something to it. If it works, its an `lvalue`, otherwise it is not.
```cpp
void check(int& x){};

int main(){

	int x = 10;
	const int& y = 1;
	
	check(10); // will not work
	check(x); // will work
	check(y); // will not work
	check((int&) y); // will work but not recommended
	
	return 0;
}
```
## Examples
### Example 1
- Here, everything on the left is an `lvalue` and everything on the right is an `rvalue`
```cpp
void print(string& s){
	cout << s << endl;
}

int main(){

	string s1 = "lvalue";
	string s2 = "rvalue";
	string s3 = s1 + s2; // rhs is an rvalue therefore below function call will not work
	
	print(s1 + s2); // will not work
	return 0;
}
```

### Example 2
#### Case 1: Passing `const int x` to a Function Expecting `int`

```cpp
void foo(int x) {
    // Function body
}

int main() {
    const int y = 10;
    foo(y);  // Works fine
    return 0;
}
```

#### Case 2: Passing `const int& x` to a Function Expecting `int&`

```cpp
void foo(int& x) {
    // Function body
}

int main() {
    const int y = 10;
    foo(y);  // Error: cannot bind non-const lvalue reference to a const int
    return 0;
}
```

#### Why Does Case 1 Work?

In the first case, the function `foo(int x)` expects an `int`, which means it's expecting a copy of the value. When you pass `y` (which is a `const int`) to `foo`, the compiler creates a copy of `y`, which is an `int`, and passes that copy to the function. The `const` qualifier is only relevant for the original variable `y`, and does not apply to the copied value being passed to the function.

#### Why Does Case 2 Fail?

In the second case, the function `foo(int& x)` expects a non-const lvalue reference. An lvalue reference requires that the argument passed to it be modifiable because the reference allows the function to potentially modify the original variable.

- **`const int y`**: The variable `y` is a `const int`, meaning it cannot be modified.
- **`foo(int& x)`**: The function expects a non-const lvalue reference, meaning it needs to be able to modify the value of `x`.

When you try to pass `y` (a `const int`) to a function that expects a non-const `int&`, the compiler will throw an error because it can't guarantee that the function won't attempt to modify `y`, which would violate the `const` qualifier.

#### Key Differences

- **Copying (`int x`) vs. Referencing (`int& x`)**: 
  - In the first case (`int x`), the value is copied, so the function operates on a separate, non-const copy of the variable, which is allowed.
  - In the second case (`int& x`), the function would directly operate on the original variable, which is `const`, and that's not allowed because the function could potentially modify it.

- **Constness Enforcement**:
  - **Passing by Value (`int x`)**: The constness of the original variable is irrelevant after copying. The function just works with the copied value.
  - **Passing by Reference (`int& x`)**: The constness of the original variable matters because the function could modify it through the reference.

#### Correcting the Error

If you want to pass a `const int` to a function expecting a reference, you can change the function to accept a `const int&`:

```cpp
void foo(const int& x) {
    // Function body
}

int main() {
    const int y = 10;
    foo(y);  // Works fine
    return 0;
}
```

In this case, `foo` is allowed to accept `const int` arguments because it guarantees not to modify them.

#### Summary

- **Case 1** works because the `const int` is copied into a non-const `int`, which is perfectly fine.
- **Case 2** fails because the function expects a non-const reference, but you're trying to pass a `const` variable, which can't be modified.

### Example 3

## References