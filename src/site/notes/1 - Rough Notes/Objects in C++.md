---
{"dg-publish":true,"permalink":"/1-rough-notes/objects-in-c/"}
---


# Objects in C++

15-08-2024 17:16

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]] [[1 - Rough Notes/Classes in C++\|Classes in C++]]

## Code snippet 1

Consider this piece of code

```cpp
#include <bits/stdc++.h>

using namespace std;

class A
{
protected:
    int x = 2;
};

class B : public A
{
public:
    int x; // this is a new x. not the one inherited from A
};

int main()
{
    A *objA = new B;
    cout << objA->x; // will give error
    cout << static_cast<B*>(objA)->x; // will work
    return 0;
}
```

1. Memory Allocation:
   - The `new` operator is called to allocate memory for an object of class B.
   - This allocates enough memory to hold all members of B, including those inherited from A.

2. Constructor Calls:
   - The constructor for class A is called first. This is always the case in inheritance - base class constructors are called before derived class constructors.
   - In this case, A's default constructor is called, which initializes `A::x` to 2.
   - Then, B's default constructor is called. However, B doesn't have an explicitly defined constructor, so the compiler-generated default constructor is used.
   - B's compiler-generated constructor doesn't initialize `B::x`, so it remains uninitialized.

3. Assignment:
   - The address of the newly created B object is assigned to `objA`.
   - This is allowed because B publicly inherits from A, so a B* can be implicitly converted to an A*.
   - No conversion operator is explicitly called here; this is an implicit conversion.

4. Pointer Type:
   - Although `objA` points to a B object, its declared type is A*. This means when accessing members through `objA`, the compiler will look at A's definition, not B's.

Now, let's look at what happens with `cout << objA->x;`:

- This tries to access `x` through `objA`.
- Since `objA` is of type A*, the compiler looks for `x` in class A.
- However, `x` is protected in A, so this line will cause a compilation error.

If you wanted to access B's `x`, you would need to cast `objA` to a B pointer:

```cpp
cout << static_cast<B*>(objA)->x;
```

But note that B's `x` is uninitialized, so this would print an indeterminate value.

Key points:
1. No copy constructor or assignment operator is used in this process.
2. The initialization of `A::x = 2` happens, but `B::x` remains uninitialized.
3. The `new` operator is used once to allocate memory and call constructors.
4. There's an implicit conversion from B* to A* when assigning to `objA`.

This code demonstrates some important concepts about inheritance, member hiding, and pointer behavior in C++. It's worth noting that having a member in B with the same name as a member in A (both `x` in this case) can lead to confusion and is generally not recommended unless you have a specific reason for doing so.

## Code snippet 2
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
public:
    virtual void foo() {
        cout << "foo from A\n";
    }
};

class B : private A
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
    B b1{};
    B b2 = b1;
    B b3(b1);
    b1 = b2;

	A *objA = new B; // will not work
	B *objB = new B; // will work
    
    objB->foo(); // does not work
    ((A*)objB)->foo();  // works. It will output "foo from B". If foo was not virtual, it would output "foo from A".

    return 0;
}
```

1. `B b1{};`
   - This creates a B object using uniform initialization.
   - The default constructor of B is called.
   - Since B privately inherits from A, A's default constructor is called first, then B's.
   - No explicit constructors are defined, so compiler-generated ones are used.
   - A's virtual function table (vtable) is set up, including entries for `func()` and `foo()`.

2. `B b2 = b1;`
   - This invokes the copy constructor of B.
   - Since no custom copy constructor is defined, the compiler-generated one is used.
   - It performs a member-wise copy of b1 to b2.
   - This includes copying the vtable pointer and any members inherited from A.

3. `B b3(b1);`
   - This is another way to invoke the copy constructor, functionally identical to the previous line.
   - It creates b3 as a copy of b1, again using the compiler-generated copy constructor.

4. `b1 = b2;`
   - This calls the copy assignment operator of B.
   - Again, since no custom operator is defined, the compiler-generated one is used.
   - It performs a member-wise assignment from b2 to b1.

Key points:
- No dynamic memory allocation (`new`) is used in this `main()` function.
- The compiler-generated special member functions (default constructor, copy constructor, copy assignment operator) are used throughout.
- Despite private inheritance, B objects still contain the full A part, including its vtable.

Some more things to note:

- `A *objA = new B;` would not compile because B privately inherits from A, so B* cannot be converted to A*.
- `B *objB = new B;` would compile and work as expected, creating a B object on the heap.
- `objB->foo();` would not compile because `foo()` is private in B.

The private inheritance in this example means:
1. B inherits A's members, but they become private in B.
2. B cannot be treated as an A externally (no implicit conversions from B* to A*).
3. B can still override A's virtual functions, but they're only accessible within B.

This code structure creates a situation where B has A's interface and implementation, but doesn't expose them publicly, which can be useful for certain design patterns but requires careful handling to avoid misuse.

## References