

```markdown
# Introduction to Rust Programming Language

---

## 1. **Hello, World!**
Every Rust program starts with a `main` function.

```rust
fn main() {
    println!("Hello, world!");
}
```

- `fn main()` defines the main function, which is the entry point of the program.
- `println!()` is a macro (denoted by `!`) that prints text to the console.

---

## 2. **Variables and Mutability**
Rust variables are **immutable** by default, meaning their values cannot change.

```rust
fn main() {
    let x = 5;
    println!("The value of x is: {}", x);

    let mut y = 10; // Mutable variable
    println!("The value of y is: {}", y);

    y = 20; // Can be changed because it's mutable
    println!("The updated value of y is: {}", y);
}
```

- `let x = 5;` creates an immutable variable. This means you cannot change `x` after it's assigned.
- `let mut y = 10;` allows mutation (changing values) because it's declared with `mut`.
- Rust's immutability by default helps ensure safety and predictability in your code, reducing bugs caused by unintended modifications.

---

## 3. **Data Types**
Rust is statically typed, meaning types must be known at compile time.

```rust
fn main() {
    let int_num: i32 = 42; // Integer
    let float_num: f64 = 3.14; // Floating point
    let is_rust_fun: bool = true; // Boolean
    let letter: char = 'R'; // Character

    let text: &str = "Hello, Rust!"; // String slice (immutable)
    let mut string_obj: String = String::from("This is a String"); // Growable string

    let tuple_example: (i32, f64, char) = (100, 6.28, 'T'); // Tuple
    let array_example: [i32; 3] = [1, 2, 3]; // Fixed-size array
    let vector_example: Vec<i32> = vec![10, 20, 30, 40]; // Dynamic array (vector)
    
    let slice_example: &[i32] = &array_example[0..2]; // Slice from array

    println!("Integer: {}, Float: {}, Boolean: {}, Char: {}", int_num, float_num, is_rust_fun, letter);
    println!("String Slice: {}", text);
    println!("String Object: {}", string_obj);
    
    println!("Tuple: ({}, {}, {})", tuple_example.0, tuple_example.1, tuple_example.2);
    println!("Array: {:?}, First Element: {}", array_example, array_example[0]);
    println!("Vector: {:?}, Last Element: {}", vector_example, vector_example.last().unwrap());
    println!("Slice: {:?}", slice_example);
}
```

- **String Slice (`&str`)**: Immutable and fixed-length.
- **String Object (`String`)**: Growable, can be modified.
- **Tuple**: A fixed-size collection of different types.
- **Array**: A fixed-size list of values (e.g., `[i32; 3]` means an array of three `i32` values).
- **Vector (`Vec`)**: A dynamic array that can grow/shrink.
- **Slice (`&[i32]`)**: A reference to part of an array, without taking ownership.

---

## 4. **Control Flow**
### Conditional Statements (`if-else`)
```rust
fn main() {
    let number = 10;

    if number > 5 {
        println!("The number is greater than 5");
    } else {
        println!("The number is 5 or less");
    }
}
```

- In Rust, you don't need parentheses around conditions, but blocks (`{}`) are mandatory for the body of the `if` or `else`.

### Loops (`loop`, `while`, `for`)
```rust
fn main() {
    let mut count = 0;

    // Infinite loop (Use `break` to stop)
    loop {
        if count == 3 {
            break;
        }
        println!("Count: {}", count);
        count += 1;
    }

    // While loop
    while count < 6 {
        println!("While count: {}", count);
        count += 1;
    }

    // For loop with range
    for i in 0..3 {
        println!("For loop: {}", i);
    }
}
```

- `loop` runs indefinitely unless `break` is used.
- `while` runs as long as the condition is true.
- `for` iterates over a range (e.g., `0..3` means `0, 1, 2`).

---

## 5. **Functions**
Functions are defined using `fn` and can take parameters and return values.

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b // Implicit return (no `;`)
}

fn main() {
    let result = add(5, 10);
    println!("Sum: {}", result);
}
```

- `-> i32` indicates that the function returns an integer.
- In Rust, the last expression in a function is implicitly returned, meaning you don’t need to use the `return` keyword.

---

## 6. **Structs (Custom Data Types)**
Structs allow defining custom types.

```rust
struct Person {
    name: String,
    age: u8,
}

fn main() {
    let person = Person {
        name: String::from("Alice"),
        age: 30,
    };

    println!("{} is {} years old", person.name, person.age);
}
```

- A `struct` defines a custom data type with named fields. Here, `Person` has fields `name` and `age`.
- `String::from()` creates a `String` from a string literal. This is necessary because Rust uses a special `String` type for dynamic, heap-allocated strings, while string literals (`&str`) are immutable and stored in the program’s binary.

---

## 7. **Enums and Pattern Matching**
Enums define a type with multiple possible variants.

```rust
enum Direction {
    Up,
    Down,
    Left,
    Right,
}

fn move_direction(dir: Direction) {
    match dir {
        Direction::Up => println!("Moving up"),
        Direction::Down => println!("Moving down"),
        Direction::Left => println!("Moving left"),
        Direction::Right => println!("Moving right"),
    }
}

fn main() {
    let my_direction = Direction::Left;
    move_direction(my_direction);
}
```

- `enum` defines a type that can have multiple values, known as variants. Here, `Direction` can be `Up`, `Down`, `Left`, or `Right`.
- `match` is used for pattern matching, replacing long `if-else` chains. It allows checking the variant and performing an action based on it.

---

## 8. **Ownership & Borrowing**
Rust ensures memory safety through ownership rules.

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1; // Ownership moves from s1 to s2

    // println!("{}", s1); // This would cause an error because s1 is invalid now.

    let s3 = String::from("hello");
    let s4 = &s3; // Borrowing (s3 is still valid)
    println!("s3: {}, s4: {}", s3, s4);
}
```

- **Ownership**: In Rust, when a variable is assigned to another, ownership is transferred. After `s1` is moved to `s2`, `s1` becomes invalid.
- **Borrowing**: Instead of transferring ownership, borrowing allows the variable to be used without taking ownership. Here, `&s3` borrows `s3`.

---

## 9. **Vectors (Growable Arrays)**
Vectors store lists of values dynamically.

```rust
fn main() {
    let mut numbers = vec![1, 2, 3, 4];

    numbers.push(5); // Add an element
    println!("Numbers: {:?}", numbers);

    let first = numbers[0]; // Access an element
    println!("First number: {}", first);
}
```

- `vec![]` creates a vector. Unlike arrays, vectors are growable.
- `.push()` adds elements to the vector.
- `{:?}` in `println!()` prints the debug output for vectors, arrays, and other types that implement the `Debug` trait.

---

## 10. **Error Handling (Result & Option)**
Rust uses `Result` and `Option` for error handling.

```rust
fn divide(a: f64, b: f64) -> Result<f64, String> {
    if b == 0.0 {
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(a / b)
    }
}

fn main() {
    match divide(10.0, 2.0) {
        Ok(result) => println!("Result: {}", result),
        Err(error) => println!("Error: {}", error),
    }
}
```

- `Result<T, E>` is used for functions that can return a success (`Ok`) or an error (`Err`).
- `Option<T>` is used when a value might be present (`Some`) or absent (`None`).
- `match` is commonly used for handling `Result` and `Option`, making error handling explicit and safe.

---

## 11. **Concurrency (Threads)**
Rust supports safe concurrency with threads.

```rust
use std::thread;
use std::time::Duration;

fn main() {
    let handle = thread::spawn(|| {
        for i in 1..5 {
            println!("Thread: {}", i);
            thread::sleep(Duration::from_millis(500));
        }
    });

    handle.join().unwrap(); // Wait for the thread to finish
}
```

- `thread::spawn()` creates a new thread to execute code concurrently.
- `handle.join()` waits for the thread to finish, ensuring that the main thread does not exit before the spawned thread.

---
``` 
