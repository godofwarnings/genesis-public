---
{"dg-publish":true,"permalink":"/1-rough-notes/classes-in-c/"}
---

# Classes in $C++$

27-07-2024 15:35

Status: 

Tags: [[3 - Tags/CPP\|CPP]] [[3 - Tags/OOPS\|OOPS]]

### Structs vs Class
- technically, there is no difference between a `struct` and a `class` apart from the fact that everything in  a class is private by default and everything in a `struct` is public by default. If you were to replace class with struct, everything would work just fine.
- The difference more or less arises in semantics. In $C++$, structs mainly exist to maintain backwards compatibility with C. 
- It all boils down to your style of programming. Usually people would use structs if all they want is to collect a bunch of variables together. It would not contain massive amount of functionality


## References