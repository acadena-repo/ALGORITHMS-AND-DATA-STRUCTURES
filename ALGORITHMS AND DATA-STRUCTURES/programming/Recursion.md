<h1 align="center">Programming Paradigms</h1>
<h2 align="center">Recursion</h2>

<br><br>  
# _Table of Contents_

- [Overview](#id01)
- [Types of Recursion](#id02)
- [Tail Recursion and Iteration](#id03)
- [Exercises](#id04)

<a id='id01'></a>
# Overview
`Recursion` is a method where the solution to a problem depends on solutions to **smaller instances of the same problem**, namely we break the task into smaller subtasks until we hit a `base case`.  
**NB: we must to define a `base cases` in order to avoid infinite loops (_stack overflow_).**

It must be notice that any problem tha can be solved with recursion can be solved with iteration and vice versa.

For example, if we want to sum the first $n$ numbers:

```python
# Using iteration
def sum_numbers(n):
    result = 0

    for num in range(1, n + 1):
        result += num

    return result
```
```python
# Using recursion
def sum_numbers(n):
    # we define a base case
    if n == 1:
        return 1

    return n + sum_numbers(n - 1)
```

<a id='id02'></a>
# Types of Recursion

Depend on where the recursive function is called there are two types of recursion:

- `Tail Recursion`: It's when the recursive function call occurs at the end of the function, so `tail recursion` executes all the statements _before jumping to next recursive call_ . The most important takeaway is that tail recursion is similar to a **for or while loop.**  
- `Head Recursion`: It's when the recursive function call occurs at the biginning of the function, so `head recursion` saves the **sate** of the function call (_parameters and function variables_) before jumping to the next recursive call. Due to this condition, head recursion needs _more memory (stack memory) because of the states it stores_.

Because of this fundamental difference between head recursion and tail recursion, we should be aware of implement tail recursion method to optimize the use of the stack memory.

Due to `head recursion` function calls, uses values returned from other function calls **it creates dependency on each other** and forcing to keep each function call in the stack memory until we reach the `base case`.

This codition can be optimized using `tail recursion`, where related function calls do not depend on each other (_there is no "downward dependence"_), namely the function calls and stack frames are totally independent of each other.

```python
# factorial using head recursion
# notice that the function needs the result 
# of the recursive call to calculate its product
def factorial(n):
    # we define a base case
    if n == 1 or n == 0:
        return 1

    return n * factorial(n - 1)
```
The `factorial` function can be "changed" to tail recursion adding a parameter that "tracks" the product on each recursive call which allows decoupling the dependency among calls.

```python
# factorial using tail recursion
# notice that we add a parameter to track the result
def factorial(n, result = 1):
    # we define a base case
    if n == 1 or n == 0:
        return result

    return factorial(n - 1, n * result)
```

**NB: for the tail recursion implementation it can be notice that we can remove the `return` keyword (_we can substitute it with a print statement_) and the implementation will work fine, because the recursive function does not depend on other calls. For the case with head recursion the `return` keyword cannot be removed because previous calls must return its value in order to calculate the result.**

```python
def factorial(n, result = 1):
    # we define a base case
    if n == 1 or n == 0:
        print(result)
        return # end condition for the recursive calls
    factorial(n - 1, n * result)
```

<a id='id03'></a>
# Tail Recursion and Iteration
With the use of the `accumulator` technique an algorithm that is expressed as iteration can be transformed into tail recursion.

Remember that tail recursion is similar to a loop, where each operation is executed in the stack memory.

As an example, we can implement a function that retunrs the $n$ _Fibonacci_ number in the sequence with the use of tail recursion and iteration.

```python
# Using iteration
def fibonacci(n):
    # we define the first two fibonacci numbers
    fib1, fib2 = 0, 1

    if n == 1:
        return fib1
    if n == 2:
        return fib2

    for _ in range(n - 2):
        # calculate the next number in the sequence
        fibx = fib1 + fib2
        # update the next numbers in the sequence
        fib1, fib2 = fib2, fibx

    return fibx
```
```python
# Using tail recursion
def fibonacci(n, fib1=0, fib2=1):
    # we define a base case
    if n == 1:
        return fib1
    if n == 2:
        return fib2
    
    fibx = fib1 + fib2
    return fibonacci(n - 1, fib2, fibx)
```
**NB: a more optimal solution to calculate the fibonacci sequence is not with recursion but with memoization which is a technique that `Dynamic Programming` uses.**

Recursion is a poweful technique to use for problems that can be subdivided using a common approach, namely setting a common procedure that we can use on each recursive call.

As a use case, the `Euclidean Algorithm` which is an efficient method to calculate the _Greater Common Divisor_ of two integers.  
**NB: GCD is the largest number which divides both integers without remainder.**

Giving two integer numbers $a$ and $b$ where $a \ge b$, the largest number can be expressed as: $a = b * q + r_0$, where $q$ is a quotient and $r_0$ is a remainder. This expression can be extended to the smaller of the two initial integers as: $b = r_0 * q + r_1$.

Using this approach we can construct a function that can calculate the `GCD` as a recursive procedure:  
$n_1 = n_2 * q_0 + r_0$  
$n_2 = r_0 * q_1 + r_1$  
$r_0 = r_1 * q_2 + r_2$  
$r_{n-1} = r_n * q_{n+1} + r_{n+1}$

When the remainder $r_{n+1} = 0$, then the remainder $r_n$ = _`GCD`_.

```python
def gcd(a, b):
    # we first validate a >= b
    if a < b:
        return 1
    # we define a base case
    if a % b == 0:
        return b

    return gcd(b, a%b)
```
And because it is a tail recursion implementation an iterative solution can be derived.
```python
def gcd(a, b):
    # we first validate a >= b
    if a < b:
        return 1

    while a%b != 0:
        a, b = b, a%b

    return b
```

As a conclusion, it seems the use of recursion or iteration is a matter of preference, but what is the real difference to guide us in the use of recursion or iteration?
- ` Is the ability to modify values during operation`

In `tail recursion` stack frames are totally independet of each other, so every recursive call gets its own stack frame (_with its own local variables_) which is isolated from the other recursive calls, then **recursive calls cannot change the values of the variables**.

By the other hand, during iteration its is possible to change, update or remove values in the data structure (_an array for example_).

`This main difference must be evaluated before our solution implementation.`

<a id='id04'></a>
# Exercises

## Linear Search:
Return the `index` of the number we want to search for in an **unordered** array of numbers.  
$numbers = [2,8,45,73,6,12,2,7,55,36]$

```python
def linear_search(numbers, target):
    return linear_search_recv(numbers, target)

def linear_search_recv(array, target, idx=0):
    # we define a base case
    if idx > len(array) - 1:
        return

    if array[idx] == target:
        return idx
    else:
        return linear_search_recv(array, target, idx + 1)
```
Linear search has $O(N)$ linear running time complexity and $O(N)$ space complexity due to in the worse case we will have $N$ stack frames. Can we do better?, yes but we need to _sort_ the array.

## Binary Search:
Return the `index` of the number we want to search for in a **sorted** array of numbers.
$numbers = [-4,-1,0,2,4,7,12,24,34,52]$

```python
def binary_search(numbers, target):
    return binary_search_recv(numbers, target, 0, len(array) - 1)

def binary_search_recv(array, target, left, right):
    # we define a base case
    if left > right:
        return

    # calculate the middle point of the array
    middle = (right + left)//2
    # check for target to delimit the side of the subarray
    if array[middle] > target:
        # target is in the left subarray
        return binary_search_recv(array, target, left, middle - 1)
    elif array[middle] < target:
        # target is in the right subarray
        return binary_search_recv(array, target, middle + 1, right)
    else:
        # we found the value
        return middle
```
Binary search improves the running time complexity to $O(logN)$ but we must provide to the algorithm a sorted array. It must be notice that sort operation with an efficient algorithm takes in average $O(NlogN)$, so if we have an **unordered** array and want to apply binary search we will finish with a $O(NlogN)$ running time complexity, much bigger that linear search running time complexity.

## Selection Algorithms
`Selection Algorithms` are algorithms used to find the $k^{th}$ order statistic which is the $k^{th}$ smallest (_or largest_) item in a data structure. We can find the `maximum`, the `minimum` or the `median` items.

Notice that looks a similarity between `selection algorithms` and `search algorithms`, so a question pops. Can we use _binary search_ as an approach?

Selection algorithms aims to achieve $O(N)$ running time complexity such as `quickselect` or `median-of-medians`. Remember that in order to use binary search the data structure must be ordered and average running time complexity of sorting algorithms is $O(NlogN)$ which is higher than linear running time complexity.

So as a rule-of-thumb we can say that it is inefficient use sorting if we only need to find the $k^{th} order \space statistic = 1$, which is a single item (_maximum, minimum or median_), but it can be efficient to sort the data structure if we need to find **several $k^{th}$ order statistics**.

### _Quickselect Algorithm_
It is a selection algorithm designed by Tony Hoare and it is used to find the $k^{th}$ smallest or largest item in an unordered array.

It has $O(N)$ running time in best-case and $O(N^2)$ in the worse-case. The algorithm uses an in-place approach so it has $O(1)$ space complexity.

**Algorithm Definition:**
- Choose a `pivot` item (_can be at random_)  
- Partition the array base on the value of the `pivot` (_Partitioning Phase_)  
We select an item in the array and use it to swap smallest values than the pivot to the left and largest to the right.
- We search for the item in one side of the array recirsively (_Select Phase_)  
After the partitioning we may deal with 3 cases:  
1. $k = pivot$. We find the item. **Notice that there are $k - 1$ items that are smaller than the pivot.**  
2. $k > pivot$. The $k^{th}$ smallest item is at the right of the pivot. Then we only need to focus on the right subarray.  
3. $k < pivot$. The $k^{th}$ smallest item is at the left of the pivot. Then we only need to focus on the left subarray.

```python
import random

class QuickSelect:

    def __init__(self, array):
        self.array = array
        # set the indices according with the array length
        self.left = 0
        self.right = len(array) - 1

    def get_kth_statistic(self, k, largest=False):
        self.type = largest
        return self.select(self.left, self.right, k-1)

    def partitioning(self, first_idx, last_idx):
        # select a pivot item randomly
        pivot = random.randint(first_idx, last_idx)

        # swap pivot with last value in the array
        self.swap(pivot, last_idx)
        # partitioning of the array into left < pivot < right
        for x in range(first_idx, last_idx):
            # we want largest kth order statistic
            if self.type:
                if self.array[x] > self.array[last_idx]:
                    self.swap(x, first_idx)
                    # update next position for swap
                    first_idx += 1
            else:
                if self.array[x] < self.array[last_idx]:
                    self.swap(x, first_idx)
                    # update next position for swap
                    first_idx += 1

        # move pivot item between left and right subarrays
        self.swap(last_idx, first_idx)
        # return the index of the pivot value
        return first_idx

    def swap(self, source, dest):
        self.array[source], self.array[dest] = self.array[dest], self.array[source]

    def select(self, first_idx, last_idx, k):
        # get the pivot index
        pivot_idx = self.partitioning(first_idx, last_idx)

        # check for item
        if k > pivot_idx:
            # look for item in right subarray
            return self.select(pivot_idx + 1, last_idx, k)
        elif k < pivot_idx:
            # look for item in left subarray
            return self.select(first_idx, pivot_idx - 1, k)
        else:
            # then we found the item
            return self.array[pivot_idx]
```
As a `Tip`, we can use quickselect to sort an array using a simple for loop.
```python
array = [1, 2, -5, 10, 100, -7, 3, 4]
quicksel = QuickSelect(array)
sorted_array = []
# because we decrement the kth by one
for x in range(1, len(array) + 1):
    sorted_array.append(quicksel.get_kth_statistic(x))

```
**NB: quickselect algorithm is quite sensitive to the pivot selection which we used to discard the maximum number of items in each iteration. If for example, we select the largest number in each iteration and we are looking for the smallest value we will finish with $O(N^2)$ time complexity.**

## Bit Manipulation
Before applying recursion on _bit manipulation problems_ we need to do a quick review on bit operation in python.

**Bit Operations in Python**
- `AND` operand: _"&"_  
e.g.: 27 & 12 = 8  
1 1 0 1 1  
0 1 1 0 0  
0 1 0 0 0

- `OR` operand: _" | "_  
e.g.: 27 | 12 = 31  
1 1 0 1 1  
0 1 1 0 0  
1 1 1 1 1

- `XOR` operand: _" ^ "_
e.g.: 27 ^ 12 = 23  
1 1 0 1 1  
0 1 1 0 0  
1 0 1 1 1  
**NB: notice that XOR operator by 1 _increaments by 1_ any even number and _decrement by 1_ any odd number.**
```python
def is_even(num):
    if num ^ 1 == num + 1:
        return True
    return False
```
- `LEFT SHIFT` operand: _" << "_
e.g.: 27 << 2 = 108  
_ _ 1 1 0 1 1  
1 1 0 1 1 0 0  
**NB: notice that `left shift` doubles the original value (_$num * 2$ every shift_)**

- `RIGHT SHIFT` operand: _" >> "_
e.g.: 27 >> 2 = 6  
1 1 0 1 1  
0 0 1 1 0
**NB: notice that `right shift` divides the original value by 2 (_$num // 2$ every shift_)**  
**NB: notice that `right shift` reduce by half the original number then it has $O(logN)$ time complexity.**

```python
# with the use of right shift we can count the number
# of bits needed to represent any integer number
def count_bits(number):
    counter = 0
    while number > 0:
        number = number >> 1
        counter += 1

    return counter
```
- `Binary Representation` for an integer: _bin(integer)_  
e.g.: bin(27) = '0b11011'

### _Russian Peasant Multiplication_
Russian peasant multiplication is a way to multiply numbers that uses a process of `halving` and `doubling` without using multiplication operator. The idea is to double the first number and halve the second number till the second number doesn't become 1.  
e.g.: $64 * 20 = 1280$  
64      20  
32      40  
16      80  
 8      160  
 4      320  
 2      640  
 1      1280  

 ```python
 # using the left shift and right shift operations
 # we can implement the russian peasant multiplication
 def russian_mult(a, b):
    # set the condition to stop algorithm
    while b > 1:
        # we double the first number
        a <<= 1
        # we halve the second number
        b >>= 1
    return a
```
```python
# russian peasant multiplication with recursion
def russian_mult(a, b):
    # we define a base case
    if b == 1:
        return a
    return russian_mult(2*a, b//2)
```