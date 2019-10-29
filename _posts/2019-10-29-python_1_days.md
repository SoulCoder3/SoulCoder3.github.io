---
layout:     post
title:      Python_learn_1_days
subtitle:   
date:       2019-10-29
author:     BY
header-img: img/post-bg-kuaidi.jpg
catalog: true
tags:
    - python


---

## Python-1-days

##for-in  

Example1:

```python
'''
Use For-in to achieve even summation between 1~100
'''

sum = 0
for i in range(2,100,2):
	sum += i
print(sum)
```

* **range(101)** can create a sequence of integers from 0 to 100
* **range(1,100)** can create a sequence of integers from 1 to 99
* **range(1,100,2)** can create a odd sequence of 1 to 99, where 2 is the step size

Example2:

```python
'''Enter a positive integer to determine if it is a prime number'''
from math import sqrt

def is_prime(num):
    end = int(sqrt(num))
    if num<= and &num>1:
        return False
    if num % 6 != 1 and num % 6 != 5:
        return False
    for x in range(5, end + 1, 6):
       if num % x == 0 or num % (x+2) == 0:
           return False
    return True

num = int(input('please input a postive integer: '))
if is_prime(num):
    print('is prime')
else:
    print('not prime')

```

**if a number is a prime number, it must equal to 6x-1 or 6x+1, where x is a natural number greater than or equal to 1.  ** 

---

## String

```python
str1 = 'hello, world!'
# Calculate the length of the string by the built-infunction len
print(len(str1)) # 13
# Get a copy of the first letter of the string
print(str1.capitalize()) # Hello, world!
# Get a capitalized copy of the first letter of each word in the string
print(str1.title()) # Hello, World!
# Get a copy of the string after capitalization
print(str1.upper()) # HELLO, WORLD!
# Find the location of the substring from the string
print(str1.find('or')) # 8
print(str1.find('shit')) # -1
# Similar to find but an exception is thrown when the substring is not found
# print(str1.index('or'))
# print(str1.index('shit'))
# Check if the string starts with the specified string
print(str1.startswith('He')) # False
print(str1.startswith('hel')) # True
# Check if the string ends with the specified string
print(str1.endswith('!')) # True
# Center the string at the specified width and fill the specified characters on both sides
print(str1.center(50, '*'))
# Put the string to the rigth of the specified width to the left to fill the specified character
print(str1.rjust(50, ' '))
str2 = 'abc123456'
# Check if the string is composed of the numbers
print(str2.isdigit())  # False
# Check if the string is composed of the letters
print(str2.isalpha())  # False
# Check if the string is composed of numbers and letters
print(str2.isalnum())  # True
str3 = '  jackfrued@126.com '
print(str3)
# Get a copy of the string after trimming the left and right spaces
print(str3.strip())

```

After Python 3.6, formatting string have a more concise way of writing the string f in front of the string. We can use the following syntax to simplify the code.

```python
a,b = 555, 318
print(f'{a}*{b}={a*b}')
```

---

## List

The function of travering list elements

```python
# Travering list elements by index
for index in range(len(list1)):
    print(list1[index])
# Travering list elemtns by for
for elem in list1:
    print(elem)
# Processing the list by enumberate and then traversing can get the element index and value at the same time
for index, elem in enumerate(list1):
    print(index, elem)
```

The generated synatx to create a list

```python
# After creating a list with this synatx, the element is ready, so it takes a lot of memory space
f = [x ** 2 for x in range(1, 1000)]
print(sys.getsizeof(f))  # 9043
print(f)

# the code below creates a list of generator obejcts instead of a list
# Through the generator can get the data but it does not take up extra space to store the data
# Get data through internal calculations every time you need data
f = (x ** 2 for x in range(1, 1000))
print(sys.getsizeof(f))  # 128
print(f)
```



---

## Yield

The yield statement suspends function’s execution and sends a value back to caller, but retains enough state to enable function to resume where it is left off. When resumed, the function continues execution immediately after the last yield run. This allows its code to produce a series of values over time, rather them computing them at once and sending them back like a list.

**Return** sends a specified value back to its caller whereas **Yield** can produce a sequence of values. We should use yield when we want to iterate over a sequence, but don’t want to store the entire sequence in memory.

Example:

```python
def fib(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
        yield a


def main():
    for val in fib(20):
        print(val)


if __name__ == '__main__':
    main()
```

​	it create a fibonacci sequence but it is not stored in memory.

**We alreay have a data structure like a list. Why do we need a type like tuple?**

* **Thread safe**  An invariant object can be conveniently shared access, because it can't be  modified, which can avoid unnecrssary program errors caused by this. If we don't need to add, remove, change the elements, the tuple is more suitable.
* **Tuple is better than list in both creation time and occupied space**



***

# @Property

​	We can use @property to decorate a function, which can make the function to use as a property.

Exam1:

```python
class Exam(object):
    def __init__(self, score):
        self._score = score

    @property
    def score(self):
        return self._score

    @score.setter
    def score(self, val):
        if val < 0:
            self._score = 0
        elif val > 100:
            self._score = 100
        else:
            self._score = val
>>> e = Exam(60)
>>> e.score
60
>>> e.score = 90
>>> e.score
90
>>> e.score = 200
>>> e.score
100
```

​	At this point, a new decorator score.setter is created, wich can be used to assign as a property.

***

