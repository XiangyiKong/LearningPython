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


$ python bisect_example.py

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
$ python bisect_example2.py

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