---
{"dg-publish":true,"permalink":"/1-rough-notes/virtual-in-c/"}
---

# Virtual in $C++$

28-07-2024 00:19

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]] [[Polymorphism\|Polymorphism]] [[1 - Rough Notes/Access Specifiers and Visibility in C++\|Access Specifiers and Visibility in C++]]

## Virtual Functions in $C++$
- dynamic dispacth
- if you want to override (not overload) a function, you have to mark the base function as `virtual` in the base class
- vtable. when we use `virtual` keyword, a vtable is generated for that function which stores mapping of the overridden functions (in the child classes). 
- note that this comes with a cost. the cost of memory. the vtable needs to be stored. The class with virtual function has a hidden vptr pointing to a vtable for virtual methods. This vptr imposes a high alignment requirement for the simple class, resulting in a larger size than expected.
- it also comes with a performance issue since during runtime, the system will have to go through the vtable and find the right function
- E.g if you have an embedded system with a terrible performance, where every cpu cycle counts, there you would not want to use run-time polymorphism (the virtual function)

![[Pasted image 20240728005443.png \| center ]]

## Some trick questions
### 1. The virtual function in the base class is private but one in the child class is public
```cpp nums
#include <bits/stdc++.h>

using namespace std;

class A
{
private:
    virtual void func()
    {
        cout << "Im from A\n";
        return;
    }
};

class B : public A
{
public:
    void func()
    {
        cout << "Im from B\n";
        return;
    }
};

int main()
{
    A *objA = new B;
    objA->func();

    return 0;
}
```
This will not compile. This will give the following error
```js
error: ‘virtual void A::func()’ is private within this context
```
#### The Problem
- Virtual Functions and Inheritance:
    - When a base class declares a function as `virtual`, it allows derived classes to override that function.
    - This enables polymorphism, where a pointer to the base class can call the appropriate function based on the actual object type it points to.
- The Problem in the Code:
    - In class A, `func()` is declared as `private virtual`.
    - Being `private` means it can only be accessed within class A itself.
    - Even though it's `virtual`, its `private` status prevents it from being accessed or overridden by derived classes.
- Attempted Override in Class B:
    - Class B tries to override `func()`, but it can't actually override A's `func()` because it can't see or access it.
    - B's `func()` is essentially a new function, not an override.
- The Main Function:
    - `A *objA = new B;` creates a B object but points to it with an A pointer.
    - `objA->func();` attempts to call `func()` through this A pointer.
    - However, A's `func()` is private, so it can't be called from main().
    - Even if it could be called, it wouldn't reach B's version because B didn't actually override A's `func()`.
#### The Solution
- Why Making A's func() Protected or Public Fixes It:
    - If `func()` in A is `protected` or `public`, B can actually override it.
    - This allows the virtual function mechanism to work as intended.
    - When called through an A pointer to a B object, it will correctly call B's version.
- The Concept of Overriding:
    - For a derived class to override a base class function:
        1. The function must be virtual in the base class.
        2. The function must be accessible to the derived class (public or protected).
        3. The function signature (name, parameters, return type) must match exactly.

### 2. The virtual function in the base class is public but one in the child class is private
```cpp nums
#include <bits/stdc++.h>

using namespace std;

class A
{
public:
    virtual void func()
    {
        cout << "Im from A\n";
        return;
    }
};

class B : public A
{
private:
    void func()
    {
        cout << "Im from B\n";
        return;
    }
};

int main()
{
    A *objA = new B;
    objA->func();
    return 0;
}
```
There is no problem with this code. It will compile and run and output
```js
Im from B
```
#### Explanation 
1. Class A:
   - `func()` is declared as `public virtual`.
   - This means it can be accessed from anywhere and can be overridden by derived classes.

2. Class B:
   - Inherits publicly from A.
   - Overrides `func()`, but declares it as `private`.
   - This is allowed in C++. A derived class can change the access specifier of a function it's overriding.

3. Main function:
   - Creates a B object and assigns its address to an A pointer (`A *objA = new B;`).
   - Attempts to call `func()` through this pointer (`objA->func();`).

4. What happens:
   - This code will compile without errors.
   - When run, it will output: "Im from B"

5. Detailed explanation:
   - The call `objA->func();` is legal because `func()` is public in A.
   - Even though `func()` is private in B, it still overrides A's `func()`.
   - When called through an A pointer, the virtual function mechanism kicks in.
   - It sees that the actual object is of type B, so it calls B's version of `func()`.
   - The private status of B's `func()` doesn't prevent this because the call is going through A's public interface.

6. Important concept - Access vs. Visibility:
   - The `private` in B affects access, not visibility for virtual dispatch.
   - Virtual function dispatch depends on the dynamic type of the object, not the access specifier.

7. Potential confusion:
   - While this works, it can be confusing. B's `func()` can't be called directly on a B object, but can be called through an A pointer.
   - This might violate the principle of least astonishment for some programmers.

8. Best practices:
   - Generally, it's clearer to keep consistent access specifiers when overriding.
   - If you need to restrict access, consider making the base function protected instead.

9. Note on design:
   - This pattern (public virtual in base, private override in derived) is occasionally used to prevent further overriding in classes derived from B, while still allowing polymorphic behavior through A pointers.

> [!note] Important
> - B's `func()` can't be called directly on a B object, but can be called through an A pointer.
> - Following will give error
> ```cpp nums
> B *objB = new B;
> objB->func();
> ```

### 3. Another example
```cpp
#include <bits/stdc++.h>

using namespace std;

class A
{
public:
    virtual void func()
    {
        cout << "Im from A\n";
        return;
    }
public:
    virtual void foo() {
        cout << "foo from A\n";
    }
};

class B : public A
{
private:
    void func()
    {
        cout << "Im from B\n";
        return;
    }

private:
    void foo() {
        cout << "foo from B\n";
    }
};

int main()
{
    A *objA = new B;
    B *objB = new B;

    objA->foo(); // works. outputs: "foo from B".
    objB->foo(); // does not work
    ((A*)objB)->foo();  // works. outputs: "foo from B"
    return 0;
}
```

## References
- [extra memory due to `virtual`](https://devblogs.microsoft.com/visualstudio/size-alignment-and-memory-layout-insights-for-c-classes-structs-and-unions/#:~:text=However%2C%20the%20class%20with%20virtual,of%20the%20predicted%208%20bytes.)
- 