https://rust-book.cs.brown.edu/ch04-01-what-is-ownership.html
Ownership enables Rust to make memory safety guarantees without needing a garbage collector. The main purpose of ownership is to manage heap data.

### What is Ownership?

Ownership is a set of rules that governs how a Rust program manages memory.

All programs have to manage the way they use a computer's memory while running. Some languages have garbage collection that regularly looks for no-longer used memory as the program runs; in other languages, the programmer must explicitly allocate and free the memory. Rust uses a third approach: memory is managed through a system of ownership with a set of rules that the compiler checks. If any of the rules are violated, the program won't compile.

Ownership addresses the problems of keeping track of what parts of code are using what data on the heap, minimising the amount of duplicate data on the heap, and cleaning up unused data on the heap so you don't run out of space.

More info on how this is implemented in [[The Stack and the Heap]]

### Ownership Rules

- Each value in Rust has an owner
- There can only be one owner at a time
- When the owner goes out of scope, the value will be dropped

