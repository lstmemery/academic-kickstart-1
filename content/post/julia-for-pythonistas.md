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



I mentioned to a friend that I was learning Julia for a project and he asked "Why?". The answer is that I need to use a library that is only being actively developed on Julia. However, there are some nice features that I'd like to share. My primary languages are Python and R so although I know some of these features are available in other languages they were surprising to me.  If you are looking for a full tutorial, I would suggest [JuliaBox](https://juliabox.com/) which gives out free Jupyter compute for Julia learners. One of the things that Julia hasn't fully developed is a very strong installation story and this is a very nice solution to getting up and going. This is mostly syntactic sugar.

## Ternary operators:

Ternary operators are a compact way of expressing if/else statements. Here's some code to detect if a number is even or odd in Python.

```python
# Python
if number % 2 == 0:
    return "Even"
else:
    return "Odd"
```

In Python you can squish this into

```python
"Even" if number % 2 == 0 else "Odd"
```



Here's the Julia equivalent as ternary operator:

```julia
(number %% 2 == 0) ? "Even" : "Odd"
```



## Broadcasting

Most data scientists will know broadcasting from the numpy and R. When the length of dimension of one array is divisible by another, numpy knows to "loop through" the shorter array.

```python
import numpy as np
A = np.arange(-4, 5).reshape((3, 3))
b = np.arange(0, 3)
A * b
```

Likewise, you can apply a function every element in a numpy array by using  `np.vectorize`.

```python
relu = np.vectorize(lambda x: x if x > 0 else 0)
relu(A)
```

Julia can do this much more succinctly:

```julia
relu = (x -> (x > 0) ? x : 0)
relu.([-1, 0, 1])
```



 