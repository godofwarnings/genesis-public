---
{"dg-publish":true,"permalink":"/1-rough-notes/destructors-in-c/"}
---

# Destructors in $C++$

27-07-2024 17:33

Status: 

Tags: [[3 - Tags/OOPS\|OOPS]] [[3 - Tags/CPP\|CPP]]

- Anytime an object gets destroyed, the destructor gets called
- if you want to uninitialize something or free some memory, destructor is how you do it
- for a heap based object, if you call delete, the destructor will be called
- for a stack based object, once the object goes out of scope, the destructor will be called
```cpp
void func(){
Entity e; // some class. constructor gets called
Entity.GetName(); // some class method
}

int main(){

	func();
	// destructor gets called as soon as the object `e` goes out of scope
}
```
- Destructors are created like this, `~className(){}`
```cpp
class Entity{
public: 
	~Entity(){
	}
}
```

- Why would you want to call a destructor, one good example is that if you allocate something on the heap, then you would need to free it in order to avoid memory leaks.
- it is not suggested to call a destructor manually. Not suggested as it would call the destructor twice. So if you have something like this, it would work since you are not deleting anything inside the destructor.
```cpp
class April {
public:
    
    April(){
        *x = 10;
    }

    April(int age, string name, int month){
        cout << "appapapa\n";
    }

    ~April(){
    }
};


int main(){
   Prank p1 = Prank(1,"asdasd"); // fastest way
   April a1; // will work since we also provided a default constructor
   a1.~April();
}
```
- **BUT** if you something like this, you will get a `free(): double free detected` error at runtime.
```cpp
class April {
public:
    
    int* x = new int;
    April(){
        *x = 10;
    }

    April(int age, string name, int month){
        cout << "appapapa\n";
    }

    ~April(){
        delete x;
    }
};



int main(){
   Prank p1 = Prank(1,"asdasd"); // fastest way
   April a1; // will work since we also provided a default constructor
   a1.~April();
}
```
> [!note]
> In both the cases, the code will get compiled but in second case, we will get a runtime error.
## References