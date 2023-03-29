# Mini projet for week 11
## Goals
The with macro is a feature in certain programming languages, such as Rust and Kotlin, that allows you to simplify the code by reducing the need to repeatedly reference the same object when calling its methods. It is particularly useful when working with complex data structures or APIs that require many method calls on the same object.

In Rust, the with macro is not a built-in macro and needs to be imported from the with_macros crate. Here is an example of how to use it:
```
use with_macros::with;

struct Person {
    name: String,
    age: u32,
}

impl Person {
    fn new(name: &str, age: u32) -> Person {
        Person {
            name: name.to_string(),
            age: age,
        }
    }

    fn say_hello(&self) {
        println!("Hello, my name is {} and I am {} years old.", self.name, self.age);
    }
}

fn main() {
    let p = Person::new("Alice", 30);

    with!(p, {
        say_hello(); // equivalent to p.say_hello()
        let name = .name; // equivalent to let name = p.name;
        .age = 31; // equivalent to p.age = 31;
    });

    println!("{} is now {} years old.", p.name, p.age);
}
```
