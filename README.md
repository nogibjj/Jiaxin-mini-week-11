# Mini projet for week 11
## Goals
The with macro is a feature in certain programming languages, such as Rust and Kotlin, that allows you to simplify the code by reducing the need to repeatedly reference the same object when calling its methods. It is particularly useful when working with complex data structures or APIs that require many method calls on the same object.

## Usage 

## Example
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

In this example, the with macro is used to simplify the code by allowing us to call methods and access fields on the Person object without having to repeat p. every time. The macro creates a new variable called p and assigns the original p object to it. Then, all subsequent method calls and field accesses are performed on this new variable.

The syntax for using the with macro is as follows:
```
with!(expression, {
    // code block
});
```

The expression is evaluated and the result is assigned to a variable that is accessible within the code block. If you want the variable to be mutable, you can use mut before the expression.

Inside the code block, you can call methods on the object using the . syntax. Field accesses are also done using the . syntax, but without the method call syntax.
