# Memory  Management

Controlled by the operating system and the programming language used to code the program.

|                  | Explicit Alloc        | Implicit Alloc     |
|------------------|-----------------------|--------------------|
| Explicit Dealloc | C `malloc, free`      |                    |
| Implicit Dealloc | Java `new, gc thread` | Python `gc thread` |

Non-deallocated memory results in  **memory leaks.** They slow down program execution and ultimately lead to program
crashes.

## Garbage  Collection

Any memory that is not reachable, or that is only reachable through other unreachable memory, is considered garbage.

- **Reference counting**  keeps track of the number of references to each object.
- **Tracing**  use a set of memory roots (typically the table of active variables and the stack) and recursively follow
  all the pointers to other objects in memory

## Memory management in C

### Memory layout for C

<img src="images/Memory  Layout  for  C  programs.png" alt="Memory  Layout  for  C  programs" width=350>

- **Text:** Read-only and typically stores the compiled machine instructions. fetched by the CPU for execution.
- **Initialized Data:** Contains initialized global and static variables.
- **Uninitialized Data:** contains uninitialized global and static variables. initialized to 0 by default. Allocated at
  runtime.
- **Heap:** Managed by the user. `malloc()` and `free()` during runtime.
- **Stack:** Works as a LIFO structure. Stores call frames for functions. Managed by OS/compiler.
- **Env Vars and CL Args:** Accessed during runtime using OS specific functions/ C standard library

### Allocation and deallocation

```c
#include "stdlib.h"

void func0(int val);

void func1(int *ptr);

void func2(int **ptr);

int c = 10;  // initialized data segment, 10
int i; // uninitialized data segment, 0
int *ptr1; // uninitialized data segment, nullptr


int main() {
    int j; // stack, random
    int *ptr; // stack, random (*ptr can cause seg fault)
    ptr1 = malloc(sizeof(int)); // uninitialized data segment -> heap, random
    ptr = malloc(sizeof(int)); // stack -> heap, random

    j = 4;
    *ptr = 4;

    func0(j); // j is still 4
    func0(*ptr); // *ptr is still 4

    // & is the address operator
    func1(&j); // j is now 5
    func1(ptr); // *ptr is now 5

    func2(&ptr); // ptr is a new pointer, *ptr is now 6

    free(ptr); // ptr is unchanged (*ptr can still access but assigning can cause heap corruption)
    free(ptr1);
    return 0;
}

void func0(int val) { // new var in the stack `func0`
    // value of the variable can not be changed
    val = 5;
}

void func1(int *ptr) { // pointer pass-by-value
    // value of the variable can be changed
    *ptr = 5;
}

void func2(int **ptr) { // pointer pass-by-reference
    // the pointer itself can be changed
    *ptr = malloc(sizeof(int));
    **ptr = 6;
}
```

## Memory management in Java

### Allocation

```java
class MemoryTest {
    private int i;

    public MemoryTest(int i) {
        this.i = i;
    }

    public static void main(String[] args) {
        int num = 1040; // primitive variable, stack
        MemoryTest mt; // reference variable, stack
        mt = new MemoryTest(num); // allocate for a MemoryTest object in heap
    }
}
```

### Efficient  Use  of  Memory

1. Minimize the amount of memory used by a program and the computational cost of allocation
2. Minimize the amount of work the garbage collector has to do and reduce the cost of deallocation

Caching increases the memory footprint of the program. It is a trade-off between memory usage and performance.

### new Operator

- **new** operator allocates memory for an object and returns a reference to it.

Class is a template giving details of state and methods.

- state: private variables
- methods: private helper methods, public API methods

### Internal  Structure  of  Java  Objects

* header
    * **Class pointer:** pointer to class information, for example, Integer or String
    * **Flags:** object shape, hash code, etc
    * **Lock:** lock variable or a pointer to a monitor object used to control concurrent access
    * **Size:** the length of the array for array-type objects

<img alt="Int Object  in  Java" src="images/Int Object in Java.png"  width=600/>

* String object encapsulates a character array.
* A fixed memory overhead of **352 bits** is added to any stored string

<img alt="String Object in Java" src="images/String Object in Java.png" width=600>

### Garbage Collection

- `gc` executes as a separate thread
- Overhead on execution time due to gc is typically up to 10%

### Temporary  Objects

`s1 + s2` is equivalent to `new StringBuilder(String.valueOf(s1)).append(s2).toString()`

- `StringBuilder` is a temporary object.
- Garbage collector will remove it after the operation is complete.

### String  Interning  and  String  Literals

- **String interning:** the process of storing only one copy of each distinct string value
- **String literals:** strings that are declared in the source code

Java maintains a pool of strings in the heap memory. The strings are checked for duplicates using their hash code.

## Summary

* An object encapsulates a data item allowing Java run-time to provide,
    * Memory management
    * Data synchronization
* It also allows (debugging) tools to analyze and visualize application.
* A 64-bit system would have a greater negative effect on memory usage.
* Scope of variables referencing objects must be carefully handled to ensure performance efficiency of gc process.
