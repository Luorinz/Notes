**Lecture 3** 

**Jan 22, 2019**

**What are Random numbers?**

In programming language, all random numbers are pseudo-random numbers. Pseudo-random means all random numbers are generated from a certain algorithm. The difference is that,  in a truly random process, all items share the same probability. It’s easier to do that in a physical way. However, in programming language, we would like to use a more effective way to get a random number. 

We use certain algorithms to generate a list of numbers and then pick one from it. The algorithm takes in an integer, which is called “seed”, and returns a list of numbers. One seed can only get one result. Therefore, we will always get the same results by using the same random algorithms and the same seed.

**Random library in python**

In Python, we use random library to generate a random number. 

```python
# Use this line if you want to use all functions in the library
import random

# Use this line if you want to use a certain function(Recommended)
from random import randint
from random import seed
from random import choice

# seed() takes in an integer as the seed
seed(1)

# randint(start, end) generates integers between start and end
# Both sides are inclusive
for i in range(5):
    print(randint(1, 10))   # Will always print 3, 10, 2, 5, 2

# If seed() takes nothing, then the seed is random
seed()
for i in range(5):
    print(randint(1, 10))   # The output varies

# choice(seq) takes in a sequence and return a random item of it
nums = [1, 2, 3, 4, 5]
print(choice(nums))     # prints a random number from 1 to 5
string = "ILovePython"
print(choice(string))   # prints a random character from the string
```



**While loop**

while something:

​	something

**Ctrl+c to get out of loop**

linux command

**+=** 

a = a + something

**Sys.argv**

import sys

**REPL**

read, execute, print, loop

**Range is a generator : details later**

range(0, 6)

**list(range())**

create a [0, 1, 2, 3, 4, 5]

**Lists are super powerful**

**Indices to access elements in a list**

list[0]

list[1]

list[1:2]

list[::-1]

**Zip**

zip two sequences