##### Link:
https://rust-book.cs.brown.edu/ch04-02-references-and-borrowing.html


### Explanation

```
let x = "some string";
let y = &x; // reference
```

A reference is like a pointer, in that it's an address we can follow to accesss the data stored at that address. Unlike a pointer, a reference is guaranteed to point to a valid value of a particular type for the life of that reference.

A reference allows us to create a value that refers to another value but does not own it. Because it does not own it, the value it points to will not be dropped when the reference stops being used.

We call the action of creating a reference **borrowing**.

A String structure contains a pointer, length and capacity. The  &String type is just a pointer, so a shallow copy of it will copy fewer bytes than a deep copy.


#### Mutable References

```
let x = "some string";
let y = &mut x; // mutable reference
```

Mutable references have one big restriction: if you have a mutable reference to a value, you can have no other references to that value.

The benefit of having this restriction is that Rust can prevent data races at compile time.

However, you may define as many immutable references as you wish. We also cannot have a mutable and immutable reference to the same value, since users of an immutable reference do not expect the value to suddenly change.

```
let x = "some string";

// this would be ok
let y = &x;
let z = &x;

// this would not be ok
let y = &x;
let z = &mut x;
```

###### Data Races

A data race is similar to a race condition, and occurs when:
- Two or more pointers access the same data at the same time
- At leaast one of the pointers is being used to write the data
- There's no mechanism being used to synchronise access to the data


#### Dangling References

Unlike in other languages, the Rust compiler guarantees that references will never be dangling. 
The below code would throw an error, because the function's return type contains a borrowed value, but there is no value for it to be borrowed from.

```
fn main() { 
	let reference_to_nothing = dangle();
}

fn dangle() -> &String {
	let s = String::from("hello");
	&s
}
```


#### Rules of References

- At any given time, you can have either one mutable reference or any number of immutable references
- References must always be valid