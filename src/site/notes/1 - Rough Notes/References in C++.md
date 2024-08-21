---
{"dg-publish":true,"permalink":"/1-rough-notes/references-in-c/"}
---


# References in C++

20-08-2024 22:47

Status: 

Tags: 

Certainly! Let's dive deep into how references work in C++.

### What is a Reference in C++?

A reference in C++ is an alias for another variable. When you create a reference, you are essentially creating a second name for an existing variable. Any operations performed on the reference are actually performed on the original variable.

#### Basic Syntax

To declare a reference, you use the `&` symbol:

```cpp
int x = 10;
int &ref = x;
```

Here, `ref` is a reference to the variable `x`. This means that `ref` and `x` are two names for the same memory location. If you change `ref`, `x` will also change, and vice versa.

### How References Work

When you declare a reference, the compiler doesn't create a new variable or allocate new memory. Instead, the reference just points to the memory address of the original variable. Therefore, changes to the reference directly affect the original variable.

Let's look at an example:

```cpp
int a = 5;
int &b = a;

b = 10;

std::cout << "a = " << a << std::endl; // Output: a = 10
std::cout << "b = " << b << std::endl; // Output: b = 10
```

In this code:

- `a` is initially set to `5`.
- `b` is declared as a reference to `a`.
- When `b` is assigned the value `10`, the value of `a` also changes to `10`.

### References vs. Pointers

References and pointers are similar in that they both allow you to work with the memory address of a variable. However, there are key differences:

1. **Syntax**: A reference uses the `&` symbol during declaration, whereas a pointer uses `*`.

   ```cpp
   int *ptr = &a;  // Pointer to a
   int &ref = a;   // Reference to a
   ```

2. **Nullability**: Pointers can be null (i.e., they can point to nothing), but references must always refer to a valid object or variable.

   ```cpp
   int *ptr = nullptr;  // Legal
   int &ref = *ptr;     // Illegal, causes runtime error if dereferenced
   ```

3. **Reassignment**: Pointers can be reassigned to point to different variables, but references cannot be reassigned after they are initialized.

   ```cpp
   int x = 10, y = 20;
   int *ptr = &x;
   ptr = &y;  // Legal

   int &ref = x;
   ref = y;  // Changes the value of x, does not rebind ref to y
   ```

4. **Dereferencing**: To access the value a pointer is pointing to, you need to dereference it using the `*` operator. References don’t need to be dereferenced; you can use them directly.

### Passing by Reference

One of the primary uses of references is in function parameters. By passing arguments by reference, you allow the function to modify the original variable:

```cpp
void increment(int &num) {
    num++;
}

int main() {
    int x = 10;
    increment(x);
    std::cout << "x = " << x << std::endl; // Output: x = 11
    return 0;
}
```

Here, `increment` takes an `int` reference as an argument. When `x` is passed to the function, `num` becomes a reference to `x`. Thus, modifying `num` inside the function modifies `x`.

### References as Return Values

Functions can also return references. However, be careful when returning references to local variables, as this can lead to undefined behavior (because the local variable will be destroyed when the function returns).

```cpp
int& getReference(int &a) {
    return a;
}

int main() {
    int x = 5;
    int &ref = getReference(x);
    ref = 20;
    std::cout << "x = " << x << std::endl; // Output: x = 20
    return 0;
}
```

In this case, `getReference` returns a reference to `x`, allowing us to modify `x` outside the function.

### Const References

You can declare a reference as `const` to prevent modifications through the reference:

```cpp
int x = 10;
const int &ref = x;

ref = 20; // Error: ref is read-only
```

Const references are particularly useful for passing large objects to functions without copying them, while ensuring the object isn’t modified:

```cpp
void print(const std::string &str) {
    std::cout << str << std::endl;
}
```

### Rvalue References (Advanced)

C++11 introduced rvalue references, which allow you to bind to temporary objects (rvalues) that are about to be destroyed:

```cpp
int &&rref = 10;
```

Rvalue references are primarily used in move semantics and perfect forwarding, enabling more efficient handling of resources by transferring ownership instead of copying.

### Summary

- **Reference**: An alias for an existing variable.
- **Syntax**: `int &ref = x;`
- **References vs. Pointers**: References are safer but less flexible.
- **Pass by Reference**: Allows functions to modify the original argument.
- **Const References**: Prevent modification, useful for large objects.
- **Rvalue References**: Allow binding to temporary objects for move semantics.

### Returning references as return value

- One reason you might return a reference value is if the function has a local static variable and you want to access it out of that function
```cpp
int& func(){
	static int x = 10;
	cout << x << '\n';
	return x;
}

int main(){

	int& ref = func();
	ref++;
	func();
	
	return 0;
}
```
This will OUTPUT
```js
10
11
```

### Some examples
#### Example 1
- **`int x = 5;`**: Inside the function, a local variable `x` is declared and initialized to `5`.
    
- **`int& y = x;`**: This declares a reference `y` that refers to `x`. Now, `y` is an alias for `x`, meaning `y` and `x` are the same variable. Any change to `y` will also change `x`.
    
- **`int &z = y;`**: This declares another reference `z` that refers to `y`. Since `y` is already a reference to `x`, `z` effectively becomes another alias for `x`. So, `x`, `y`, and `z` all refer to the same memory location.
```cpp
int x = 5;
int& y = x;
int &z = y;
```

## References