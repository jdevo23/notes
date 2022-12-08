Further reading:
https://rust-book.cs.brown.edu/ch04-01-what-is-ownership.html

### Intro

In order to support a mutable, growable piece of text, we need to allocate an amount of memory on the heap, unknown at compile time, to hold the contents.

```
// type of a known size, does not need to stored on the heap and referenced
let s = 0;

// type of unknown size, memory needs to be allocated on the heap
let s = String::from("Hello World");
```

This means:
	- Memory must be requested from the memory allocator at runtime
	- We need a way of returning this memory to our allocator when we're done with our String

The first part is done automatically by the String::from call. The second, in languages with a garbage collector, is done automatically. In languages without a GC, it's up to the programmer, a historically difficult task.

If we forget, we waste memory.
If we do it too early, we'll have an invalid variable.
If we do it twice, we produce a bug.

We need to pair each allocate with a free.


### Implementation

In Rust, the memory is automatically returned once the variable that owns it goes out of scope.

When a variable goes out of scope, Rust calls a function called  ```drop``` to return the memory.

A  ```String```  type is made up of 3 parts:

| Syntax      | Description | 
| ----------- | ----------- |
| ptr         |      ->     |
| len         |      5      |
| capacity    |      5      |

the pointer (ptr) points to:

| index       | value       | 
| ----------- | ----------- |
| 0         |      h     |
| 1         |      e      |
| 2    |      l      |
| 3    |      l      |
| 4    |      o      |


```
let x = String::from("hello");
let y = x;
```

When we assign y to x, the String data is copied, meaning the pointer, length and capacity. x and y both point to the same object in memory. The heap data ("hello") is not copied.

If x and y go out of scope, they will try to free the same memory. Known as a double free error, freeing memory twice can lead to memory corruption and security vulnerabilities.

To ensure memory safety, in the example x becomes invalid after y is initialised. Trying to use x will result in a error.

In the following example however, x will be valid because it is a type with a known size at compile time, which is stored on the stack, so copies of the actual values are quick to make.

```
let x = 10;
let y = x;
```

