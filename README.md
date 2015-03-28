# CircularArrays.jl

Circular Arrays implementation in Julia.

## What is this for?

Useful for implementing queues of future events with some max delay. See [this article](http://en.wikipedia.org/wiki/Circular_buffer)

## Usage:

```julia
using CircularArrays
x = reshape([i for i in 1:15],3,5)
carray = CircularArray(x)
advance_head!(carray,2)
getindex(carray,1:2,2:5) == [10 13 1 4; 11 14 2 5];
true
```

You can use regular slicing syntax as well:
```
carray[1:2,2:5] == [10 13 1 4; 11 14 2 5]
true
```

Here's another example:
```julia
using CircularArrays
c2 = CircularArray(reshape([i for i in 1:28],4,7))
advance_head!(c2,3)
setindex!(c2,[3:6],1:4,3)
c2.data == 
[1  5   9  13  17  3  25; 
 2  6  10  14  18  4  26; 
 3  7  11  15  19  5  27; 
 4  8  12  16  20  6  28]

true
```

CircularArrays works with any array type, of any number of dimensions. You can specify which dimension is the circular one.

```julia
using CircularArrays
cdim = 1
X = falses(4,3,5)
C = CircularArray(X,cdim)
advance_head!(C,1)
C[1,1:3,1:5] = trues(3,5)
reshape(C.data[2,:,:],3,5) == trues(3,5)
true
```
