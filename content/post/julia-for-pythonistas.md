+++
title = "Julia for Pythonistas"
date = 2018-12-17T18:48:42-08:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = true

+++


I mentioned to a friend that I was learning Julia for a project and he asked "Why?". The answer is that I need to use a library that is only being actively developed on Julia. However, there are some nice features that I'd like to share. My primary languages are Python and R so although I know some of these features are available in other languages they were surprising to me.  If you are looking for a full tutorial, I would suggest [JuliaBox](https://juliabox.com/) which gives out free Jupyter compute for Julia learners. One of the things that Julia hasn't fully developed is a very strong installation story and this is a very nice solution to getting up and going.

## Ternary operators:

You might have used a ternary operator in Python without knowing. Ternary operators are a compact way of expressing if/else statements. Here's some code to detect if a number is even or odd in Python.


```python
# Python
def even_or_odd(number):
    if number % 2 == 0:
        return "Even"
    else:
        return "Odd"

even_or_odd(13)
```




    'Odd'



This is ternary operator equivalent in Python. 


```python
"Even" if 13 % 2 == 0 else "Odd"
```




    'Odd'



Here's the Julia equivalent as ternary operator:


```julia
(13 % 2 == 0) ? "Even" : "Odd"
```




    "Odd"



## Broadcasting

Most data scientists will know broadcasting from the numpy and R. When the length of dimension of one array is divisible by another, numpy knows to "loop through" the shorter array. The terminology is slightly different in Julia. In Julia, broadcasting is when you apply a function to every element of an array. It's more like numpy's vectorize function.


```python
import numpy as np
A = np.arange(-4, 5).reshape((3, 3))
A
```




    array([[-4, -3, -2],
           [-1,  0,  1],
           [ 2,  3,  4]])




```python
relu = np.vectorize(lambda x: x if x > 0 else 0)
relu(A)
```




    array([[0, 0, 0],
           [0, 0, 1],
           [2, 3, 4]])



Lambdas in Julia are very succinct.


```julia
A = reshape(collect(-4:4), 3, 3)
relu = (x -> (x > 0) ? x : 0)
relu.(A)
```




    3×3 Array{Int64,2}:
     0  0  2
     0  0  3
     0  1  4



Note that I used -4:4 instead of -4:5. Julia is 1-indexed.

## Multiple Dispatch

fMultiple dispatch is a way of defining a function's behavior depending on the type of input. Imagine you need to calculate the area of a square and circle in Python.


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

    4
    13


Instead of defining an area method for each class, why not have a general area function? You can do this very easily in Julia.


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

    4.0
    13.0


At this point, I'm not sure which method I prefer. It's just a different way of doing things. I must admit that it's quite succinct.


Note: I was able to run multiple kernels in a single Jupyter Notebook with [SoS](https://vatlab.github.io/sos-docs/). 




 
