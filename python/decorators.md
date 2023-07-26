# Decorators in Python

## Functions as Objects
In Python, functions are first-class objects, which means they can be assigned to variables, passed as arguments to other functions, and returned as values from functions.

## Inner Functions
Python supports nested functions, where you can define functions inside other functions.

```python
def greet():
    print("Hello, ")

    def name():
        return "John"

    print(name())

greet()

```

## Returning Functions from Functions
You can return a function from another function, allowing you to create functions on-the-fly.

```python
def outer_function():
    print("This is outer_function")

    def inner_function():
        print("This is inner_function")

    return inner_function

my_func = outer_function()
my_func()
```

## Decorators
Decorators use the concept of nested functions to modify the behavior of other functions. They start with the `@` symbol and are placed above the function definition. When the decorated function is called, the decorator function is executed before the actual function.

```python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

Decorators provide a powerful mechanism to add functionality to functions, like logging, authentication, caching, etc., without modifying the original function's code. They are extensively used in web frameworks like Flask and Django to extend the behavior of view functions.

Advanced uses of decorators involve using arguments in decorators, creating class-based decorators, and chaining multiple decorators together. Learning decorators can significantly enhance your understanding of Python's metaprogramming capabilities and open up new possibilities in designing elegant and modular code.