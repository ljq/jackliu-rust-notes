### ownership

#### Three main Streams of Computer language Memory Management

* Garbage collection (GC) :
When a program is running, it constantly searches for memory that is no longer used. Typical examples: golang and java;

* Manual management mechanism:
Manual operation of memory allocation and release, at the language level through the method of function call to apply for and release memory, typical examples: C and C++;

* ownership Management Mechanism:
Through the ownership mechanism to manage the memory, the compiler will be compile-time according to a series of rules for relatively strict check, while avoiding excessive memory check at runtime;

#### Rust reasons for choosing an ownership mechanism

* Memory security: through clear responsibility of memory management, avoid memory preemption and sharing may bring uncertainty, relatively more secure;

* Performance: The check only happens at compile time, so there is no performance penalty for the program during runtime; Memory creation, allocation, and recycling are more efficient, eliminating the need for counting elimination mechanisms of other traditional GC languages.

#### Three Principles of ownership

* Each value in Rust is owned by a variable known as the owner of the value
* A value can only be owned by one variable at a time, or a value can only have one owner
* This value is dropped when the owner (variable) leaves the scope (drop)

#### Quotes and borrows

###### Reference: Allows the use of values but does not take ownership of them, a data pointer

###### borrowing: Obtaining a reference as a function parameter, known as borrowing, is a behavior that is not limited to variable parameter references and is commonly seen in function parameter acquisition

* References: ```&``` references that allow you to use values but do not take ownership. Pointer to the memory address of the object store
* Dereference: ```*``` dereference
* Values and references are of different types, so they cannot be directly compared
* Variable references are classified as **mutable references** and **immutable references**, function used in ```& ```or ```& mut ```distinction
Immutable reference restriction: Only one mutable reference is allowed for a particular piece of data in the same scope. The reason for this restriction is to avoid potential problems with data contention at compile time
[Data competition] Common behaviors:
* Multiple Pointers access the same data simultaneously
* At least one pointer is used to write data
* No mechanism for synchronous data access
**Mutable references** and **immutable references** cannot exist together in the same scope. The purpose of this design is to avoid data contamination caused by variable variability during reference or borrowing.

#### Dangling Dangling References

###### Dangling reference: The pointer still exists, but the memory to which the pointer points has been freed. The Rust compiler ensures that Pointers never become dangling.

###### Basic principles of reference

At any given time, either **can have only one mutable reference** or **can have only multiple immutable references**.
* References must always be valid.