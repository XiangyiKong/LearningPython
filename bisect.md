### bisect – Maintain lists in sorted order

```python
import bisect
import random

# Use a constant see to ensure that we see
# the same pseudo-random numbers each time
# we run the loop.
random.seed(1)

# Generate 20 random numbers and
# insert them into a list in sorted
# order.
l = []
for i in range(1, 20):
    r = random.randint(1, 100)
    position = bisect.bisect(l, r)
    bisect.insort(l, r)
    print '%2d %2d' % (r, position), l


python bisect_example.py

14  0 [14]
85  1 [14, 85]
77  1 [14, 77, 85]
26  1 [14, 26, 77, 85]
50  2 [14, 26, 50, 77, 85]
45  2 [14, 26, 45, 50, 77, 85]
66  4 [14, 26, 45, 50, 66, 77, 85]
79  6 [14, 26, 45, 50, 66, 77, 79, 85]
10  0 [10, 14, 26, 45, 50, 66, 77, 79, 85]
 3  0 [3, 10, 14, 26, 45, 50, 66, 77, 79, 85]
84  9 [3, 10, 14, 26, 45, 50, 66, 77, 79, 84, 85]
44  4 [3, 10, 14, 26, 44, 45, 50, 66, 77, 79, 84, 85]
77  9 [3, 10, 14, 26, 44, 45, 50, 66, 77, 77, 79, 84, 85]
 1  0 [1, 3, 10, 14, 26, 44, 45, 50, 66, 77, 77, 79, 84, 85]
45  7 [1, 3, 10, 14, 26, 44, 45, 45, 50, 66, 77, 77, 79, 84, 85]
73 10 [1, 3, 10, 14, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85]
23  4 [1, 3, 10, 14, 23, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85]
95 17 [1, 3, 10, 14, 23, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85, 95]
91 17 [1, 3, 10, 14, 23, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85, 91, 95]

If we manipulate the same data using bisect_left() and insort_left(), 
we end up with the same sorted list but notice that the insert positions are different for the duplicate values.

import bisect
import random

# Reset the seed
random.seed(1)

# Use bisect_left and insort_left.
l = []
for i in range(1, 20):
    r = random.randint(1, 100)
    position = bisect.bisect_left(l, r)
    bisect.insort_left(l, r)
    print '%2d %2d' % (r, position), l
python bisect_example2.py

14  0 [14]
85  1 [14, 85]
77  1 [14, 77, 85]
26  1 [14, 26, 77, 85]
50  2 [14, 26, 50, 77, 85]
45  2 [14, 26, 45, 50, 77, 85]
66  4 [14, 26, 45, 50, 66, 77, 85]
79  6 [14, 26, 45, 50, 66, 77, 79, 85]
10  0 [10, 14, 26, 45, 50, 66, 77, 79, 85]
 3  0 [3, 10, 14, 26, 45, 50, 66, 77, 79, 85]
84  9 [3, 10, 14, 26, 45, 50, 66, 77, 79, 84, 85]
44  4 [3, 10, 14, 26, 44, 45, 50, 66, 77, 79, 84, 85]
77  8 [3, 10, 14, 26, 44, 45, 50, 66, 77, 77, 79, 84, 85]
 1  0 [1, 3, 10, 14, 26, 44, 45, 50, 66, 77, 77, 79, 84, 85]
45  6 [1, 3, 10, 14, 26, 44, 45, 45, 50, 66, 77, 77, 79, 84, 85]
73 10 [1, 3, 10, 14, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85]
23  4 [1, 3, 10, 14, 23, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85]
95 17 [1, 3, 10, 14, 23, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85, 95]
91 17 [1, 3, 10, 14, 23, 26, 44, 45, 45, 50, 66, 73, 77, 77, 79, 84, 85, 91, 95]
```

### Searching Sorted Lists
def index(a, x):
    'Locate the leftmost value exactly equal to x'
    i = bisect_left(a, x)
    if i != len(a) and a[i] == x:
        return i
    raise ValueError

def find_lt(a, x):
    'Find rightmost value less than x'
    i = bisect_left(a, x)
    if i:
        return a[i-1]
    raise ValueError

def find_le(a, x):
    'Find rightmost value less than or equal to x'
    i = bisect_right(a, x)
    if i:
        return a[i-1]
    raise ValueError

def find_gt(a, x):
    'Find leftmost value greater than x'
    i = bisect_right(a, x)
    if i != len(a):
        return a[i]
    raise ValueError

def find_ge(a, x):
    'Find leftmost item greater than or equal to x'
    i = bisect_left(a, x)
    if i != len(a):
        return a[i]
    raise ValueError
### Other Examples
```python

The bisect() function can be useful for numeric table lookups. This example uses bisect() to look up a letter grade for an exam score (say) based on a set of ordered numeric breakpoints: 90 and up is an ‘A’, 80 to 89 is a ‘B’, and so on:

def grade(score, breakpoints=[60, 70, 80, 90], grades='FDCBA'):
        i = bisect(breakpoints, score)
        return grades[i]

[grade(score) for score in [33, 99, 77, 70, 89, 90, 100]]
['F', 'A', 'C', 'C', 'B', 'A', 'A']

Unlike the sorted() function, it does not make sense for the bisect() functions to have key or reversed arguments because that would lead to an inefficient design (successive calls to bisect functions would not “remember” all of the previous key lookups).

Instead, it is better to search a list of precomputed keys to find the index of the record in question:

>>> data = [('red', 5), ('blue', 1), ('yellow', 8), ('black', 0)]
>>> data.sort(key=lambda r: r[1])
>>> keys = [r[1] for r in data]         # precomputed list of keys
>>> data[bisect_left(keys, 0)]
('black', 0)
>>> data[bisect_left(keys, 1)]
('blue', 1)
>>> data[bisect_left(keys, 5)]
('red', 5)
>>> data[bisect_left(keys, 8)]
('yellow', 8)
```


```
