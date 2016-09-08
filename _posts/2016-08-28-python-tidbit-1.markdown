---
layout: post
title:  "Python Tidbit 1"
categories: python
---


I encountered an interesting problem when helping out a friend. I had to write a functionthat did the following:

```
#    input = [ 1, 2, 3, 4, 5, 6, ...]
#    output = [ [ 1, 2, 3 ], [ 4, 5, 6 ], ... ]

output = my_function(input)
```

Basically, I take a list, and return a list which will package up every three items into a sub-list. If there are extra elements, then drop them. Let's see what I can run with.

------------

### Potential Solutions

Fun fun fun! So how should I do this? My first thought was to do the following. It involves using the zip function, and also list slicing.

```
def my_function(input):
    return zip(input[::3], input[1::3], input[2::3])
```

Another solution that I found on stack overflow had this idea, but I think this is much less pythonic, since it requires using indices and numbers. Also, I've handled the the case where there are extra trailing inputs in the list, but this makes the xrange expression a lot more complicated.

```
def my_function(input):
    return [input[x:x+3] for x in xrange(1, len(input) - len(input) % 3, 3)]
```

But the prettiest has got to be the following. It's amazing! It took me a while to understand, but I'll try to explain it here. First, iter(input) returns an iterator to the input list. Then, I put it in a list, and multiply it by 3. What happens there is now the list has three elements, each of which is a reference to the first iterator we created. Then, we run zip on the function. When zip is run, it will call "next" on each of the elements in its argument list. Since it is a reference to the same iterator, each time the iterate will be incremented three times. I do admit, it is more confusing than my initial proposition, but I think it is very pretty! It just takes some time to get used to the syntax.

```
def my_function(input)::
    return zip( [iter(input)] * 3 )
```
