## Intro

Content from this documentation: https://rust-book.cs.brown.edu/ch04-01-what-is-ownership.html

Both the stack and the heap are parts of memory available to your code to use at runtime, but they are structured in different ways.

## Stack

The stack stores values in a last in, first out order.

## Heap

When you put data on the heap, you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a pointer, which is the address of that location. This process is called allocating on the heap, or, allocating.

## Further Explanation

Because the pointer to the heap is a known, fixed size, you can store the pointer on the stack, but when you want the actual data, you must follow the pointer. Think of being seated in a restaurant. When you enter, you state the number of people in your group, adn the staff finds an empty table that fits everyone and leads you there. If someone comes late, they can ask where you've been seated to find you.

Pushing to the stack is faster than allocating on the heap because the allocator never has to search for a place to store new data; that location is always at the top of the stack. Comparatively, allocating space on the heap requires more work, because the allocator must first find a space big enough to hold the data and then perform bookkeeping to prepare for the next allocation. A processor can do its job better if it works on data that's close to other data (as it is on the stack) rather than far away (as it can be on the heap).

When your code calls a function, the values passed into the function (including, potentially, pointers to data on the heap) and the function's local variables get pushed onto the stack. When the function is over, those values get popped off the stack.