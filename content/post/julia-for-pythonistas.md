+++
title = "Two or Three Things about Julia for Pythonistas"
date = 2018-12-17T18:48:42-08:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Julia", "Python"]
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = "/post/julia/logo.svg.png"
caption = "A few neat features of the Julia programming language."
preview = true

+++

I mentioned to a friend that I was learning Julia for a project, and he asked: "Why?". The answer is that I need to use a Julia only library. However, there are some nice features that I'd like to share. My primary languages are Python and R so although I know some of these features are available in other languages they were surprising to me.  If you are looking for a full tutorial, I would suggest [JuliaBox](https://juliabox.com/) which gives out free Jupyter compute for Julia learners. No setup is required.

## Ternary operators:

You might have used a ternary operator in Python without knowing it. A better name for the ternary operator would be "conditional expression". Ternary operators are a compact way of expressing if/else statements. Here's the way you were probably first taught an if/else statement.

```python
# Python
def even_or_odd(number):
    if number % 2 == 0:
        return "Even"
    else:
        return "Odd"

even_or_odd(13)
```

```
'Odd'
```

Here's a ternary operator in Python that does the exact same thing as before.

```python
even_or_odd = lambda x: "Even" if x % 2 == 0 else "Odd"
even_or_odd(13)
```

```
'Odd'
```

Notice the order of the statement: `"true result" if condition else "false result"`

Here's the Julia equivalent as ternary operator:

```julia
even_or_odd = x -> (x % 2 == 0) ? "Even" : "Odd"
even_or_odd(13)
```

```
"Odd"
```

In Julia, `->` is the replacement for `lambda`. Also notice that the order is slightly different: `condition? "true result": "false result".`



## Broadcasting

Most data scientists will know of broadcasting from the numpy and R. When the length of the dimension of one array is divisible by another, numpy knows to "loop through" the shorter array. The terminology is slightly different in Julia. In Julia, broadcasting is when you apply a function to every element of an array. It's more like the base `map` or numpy's `vectorize` functions. 

```python
import numpy as np
A = np.arange(-4, 5).reshape((3, 3))
A
```

```
array([[-4, -3, -2],
       [-1,  0,  1],
       [ 2,  3,  4]])
```

```python
relu = np.vectorize(lambda x: x if x > 0 else 0)
relu(A)
```

```
array([[0, 0, 0],
       [0, 0, 1],
       [2, 3, 4]])
```

Lambdas in Julia are very concise.

```julia
A = reshape(collect(-4:4), 3, 3)
relu = (x -> (x > 0) ? x : 0)
relu.(A)
```

```
3×3 Array{Int64,2}:
 0  0  2
 0  0  3
 0  1  4
```

Note that I used -4:4 instead of -4:5. Julia is 1-indexed. Did you notice the `.` after `relu`? That means "apply to each element in the array".  Julia is all about making the code as close to math as possible. What if I wanted to cube all the elements in the array before applying the `relu`?

```julia
cube = (x -> x ^ 3)
@. relu(cube(A))
```

```
3×3 Array{Int64,2}:
 0  0   8
 0  0  27
 0  1  64
```

The `@.` is a macro that applies the dot operator to all the functions on its line!



## Multiple Dispatch

Multiple dispatch is a way of defining a function's behavior depending on the type of input. In Python, we tend to make classes that implement methods that are specific to that class. Imagine you need to calculate the area of a square and circle in Python:

```python
from math import pi

class Square:
    
    def __init__(self, length):
        self.length = length
        
    def area(self):
        return self.length ** 2
    
class Circle:
    
    def __init__(self, radius):
        self.radius = radius
        
    def area(self):
        return pi * self.radius ** 2
    
square = Square(2)
print(square.area())

circle = Circle(2)
print(round(circle.area()))
```

```
4
13
```

Instead of defining an area method for each class, why not have a general `area` function? The function would need to decide what to do depending on the type of object that is used as an argument. You can do this very quickly in Julia.

```julia
struct Square
    length::Float64
end

struct Circle
    radius::Float64
end

area(shape::Square) = shape.length ^ 2
area(shape::Circle) = pi * shape.radius ^ 2

println(area(Square(2)))
println(round(area(Circle(2))))
```

```
4.0
13.0
```

At this point, I'm not sure which method I prefer. It's just a different way of doing things. I must admit that it's quite succinct.

This has been a little taste of Julia. I'm always looking for feedback. I can be reached at me@matthewemery.ca

Note: I was able to run multiple kernels in a single Jupyter Notebook with [SoS](https://vatlab.github.io/sos-docs/). 





