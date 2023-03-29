# Mini projet for week 11
<img width="248" alt="Screen Shot 2023-03-28 at 11 33 53 PM" src="https://user-images.githubusercontent.com/112274822/228419980-c96cff23-24a4-4036-b5b8-5fb2297a6ec3.png">

## Goals
The `with` macro is a feature in certain programming languages, such as Rust and Kotlin, that allows you to simplify the code by reducing the need to repeatedly reference the same object when calling its methods. It is particularly useful when working with complex data structures or APIs that require many method calls on the same object.

## Usage 
Here are some concepts related to the usage of the with macro:

1. Simplify code: The with macro simplifies code by reducing the need to repeatedly reference the same object when calling its methods or accessing its fields.
2. Reduce verbosity: By allowing you to omit the object name in method calls and field accesses, the with macro reduces the verbosity of the code and makes it more concise and readable.
3. Scope: The with macro creates a new scope in which the object is accessible, which can help to avoid naming conflicts and make the code more modular.
4. Mutable bindings: You can use the mut keyword before the object expression to create a mutable binding for the object. This allows you to modify the object within the with block.
5. Supported forms: The with macro supports three forms: method calls, variable bindings, and variable updates. Anything else is evaluated as an expression and the result is discarded.
6. Compatibility: The with macro is supported in some programming languages, such as Rust and Kotlin, but it may not be available in all languages or versions of those languages.

Overall, the with macro is a useful tool for simplifying code and reducing verbosity when working with objects that require many method calls or field accesses.

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

## Supported forms
1. `.method(args..)`: This form allows you to call a method on the object. For example, if you have an object my_obj with a method my_method, you can call the method using the with macro as follows: with!(my_obj, { my_method(arg1, arg2); });

2. `let pat = .method(args..);`: This form allows you to assign the result of a method call to a variable. For example, if you have an object my_obj with a method my_method that returns a value, you can assign the result to a variable using the with macro as follows: with!(my_obj, { let result = .my_method(arg1, arg2); });

3. `var = .method(args..);`: This form allows you to update a variable with the result of a method call. For example, if you have an object my_obj with a method my_method that updates a value, you can use the with macro to update the value as follows: with!(my_obj, { var = .my_method(arg1, arg2); });

If you use any other syntax that is not one of these three forms, it will be evaluated as an expression and the result will be discarded. For example, the following code would be valid but it would not have any effect on the object:
```
with!(my_obj, {
    42;
});
```

In this case, the expression 42 would be evaluated but the result would be discarded and no method calls or variable updates would be performed on the object.
