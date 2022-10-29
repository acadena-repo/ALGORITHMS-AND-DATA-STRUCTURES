<h1 align="center">Algorithms and Data Structures</h1>

<br><br>  

# _Table of Contents_

- [Overview](#overview)
- [Complexity Analysis](#complexity)
- [Big-O Notation](#Onotation)
- [Types of Complexities](#types)
- [Data Structures](#structures)

<br>

<a id='overview'></a>
# Overview
Software engineering in a broad sense regards with manipulating data in order to accomplish something e.g. _Developing an API which stores and retrieves data from a database and transform it in a specific format to returned to a client who’s ask for it_. So, at an elementary level software engineering is the application of operations on some sort of input data such as a list of numbers, to manipulate it in some way to perform some action such as find something, and return this piece of data.  

Then to apply software engineering two main pieces come into play:
- A data structure which supports the data structuring, organizing it, and managing it. And
- The steps need it to manipulate these data which are the operations performed, commonly known as an algorithm.

The combination of both pieces create the `program` that a computer will run. In the same general context, the computer uses its memory to store the data structure and its processing unit to execute the instructions.  

The program is a procedure that aims to solve a specific problem, but it can be notice that there may be exist multiple solutions to the same problem. A question pops from this fact, _is our solution the best possible solution?_ To answer this question a sort of comparison and analysis should be performed, that is the objective of Complexity Analysis.  

_**NB: `program` is used instead of `algorithm` to emphasise that both a set of operations and a data structure must be used in order to solve a problem.**_


<a id='complexity'></a>
# Complexity Analysis
Complexity analysis is the process of determining how efficient a program is and it usually involves finding the **space complexity** and the **time complexity** of the program.

`Space complexity` is a measure of **how much memory** a program takes up. Now a days, we can say that memory is cheap, so space complexity is not that crucial. On the other hand, `Time complexity` is a measure of **how fast** a program runs or how much time the program needs to complete its execution.

It must be noticed that time complexity is not directly related with the underlying hardware due to the same program will not run at the same time, if for example runs in a smartphone or in a supercomputer, so in order to compare two programs we should `measure the number of steps the program requires with respect to the input size`. For example, when we are dealing with _items_ we would like to sort, then of course the input size is the number of _items_ we want to sort.

We come to the conclusion that there is a **tradeoff** between memory and running time, in the sense that if we can use more memory, then we can significantly reduce running time. On the other hand, if we want to save some memory, then the running time is going to be slower, but because usually memory is cheap, we can say that running time complexity is more crucial.

Essentially running time complexity is going to define the relationship between the number of steps and the input size, establishing an order of growth, namely how the program scales and behaves with the input size.

As an example, we can say that two different programs, program `“A”` and program `“B”`, have an execution time of 100 milliseconds sorting 10 items. Once the number of items increase to 100, it notices that program `“A”` now takes 1,000 milliseconds and program `“B”` now takes 10,000 milliseconds. Then we can say that for an order of growth of 10, program `“A”` increased its execution time by 10 (linear time complexity) and program `“B”` increased its execution time by 100 (quadratic time complexity), giving as a conclusion that program `“A”` is more efficient than program `“B”`.  

Usually we are interested in large input sizes, so during our analysis we will `draw up all the terms that grow slowly and only keep the ones that grow fast` as the input size becomes larger (asymptotic analysis).

Why we don't care about the running time when the input size is equal to 10 or 100? Because even very slow algorithms are going to run extremely fast if the input size is 10 or 100, but in cases when the input size becomes larger, such as 10 million items, 100 million items and so on, it’s when, for example, linear running time complexity is way better than quadratic running time complexity.


<a id='Onotation'></a>
# Big-O Notation
Big-O notation or Landau notation, it describes the limiting behavior of a function when the argument tends towards a particular value or infinity. This is called `Asymptotic Analysis` that essentially we will draw up all the terms that grow slowly and only keep the ones that grow fast as the input size becomes larger and larger.

So essentially we would like to get a good guess about the running time of a program when the input size is large enough.

The Big-O notation is used to classify programs by how they respond in their processing requirements, namely its running time or working space, to changes in the input size.

In a more rigorous definition, Big O notation $f(n) = O(g(n))$ is a way to compare two functions $f$ and $g$. $f(n) = O(g(n))$ means, there exists a value $n_0$ > 0 and a multiplicative constant $c$ > 0 such that as long as $n$ is bigger than $n_0$, $f(n)$ will be smaller than $c * g(n)$.

<br>
<img src="./static/BIG O - GRAPH.png" alt="big-o notation"/>
<br><br>

Essentially $O(g(n))$ defines an upper bound for the $f(n)$ function. This must be taken into consideration during the complexity analysis in the sense that only the terms with higher order are kept, namely $O(g(n))$ defines the `worst case scenario` (_time or space_) for $f(n)$.

<a id='types'></a>
# Types of Complexities
<br>
<img src="./static/COMLEXITIES - GRAPH.png" alt="complexities"/>
<br><br>

$O(n!)$ – `Factorial complexity`:  
Algorithms that have factorial complexity scales with the factorial function. These algorithms are extremely slow because there is a huge amount of possible configurations. So essentially the search space is enormous and therefore these are extremely slow algorithms.

$O(C^n)$ – `Exponential Complexity`:  
Algorithms with exponential complexity scales to functions with a constant $C$ (_for example 2, 3, 4, etc._) and the input size $n$ as the exponent. These algorithms are still quite slow, so we can come to the conclusion that algorithms with factorial complexity or exponential complexity have no practical applications, due to these algorithms are extremely slow.

$O(n^k)$ – `Polynomial Complexity`:  
 Algorithms which scales to functions where $k > 1$. These algorithms are considered to be slow.

$O(n log n)$ – `Linearithmic Complexity`:  
Algorithms with these type of complexity are the first algorithms that we can say that work fine. For example, when we are dealing with sorting algorithms where brute force approaches have quadratic complexity $O(n^2)$, algorithms with linearithmic complexity do better.

$O(n)$ – `Linear Complexity`.

$O(log n)$ – `Logarithmic Complexity`.

$O(1)$ – `Constant Complexity`:  
Algorithms with constant complexity are essentially independent of the input size. For example, if we want to swap two items in an underlying one dimensional array, the swapping operation is independent of the size of the underlying one dimensional array, no matter we are dealing with 10 items or 10 billion items, the running time is going to be the same.

_Why is important to be aware of the complexity of the algorithms?_   
`Because the goal of any algorithm is to reduce the running complexity to a constant complexity, and to do so, we need to be familiar with the underlying data structures that the algorithm use to reach its goal.`  

For example, if we had an unsorted one dimensional array of integers and we want to find a given item, then we have no other option but to consider every single item one by one, and we end up with linear complexity $O(n)$. If we want to reduce the running time, we need a sorted data structure, for example, a binary tree, where we can perform a binary search and we can end up with logarithmic complexity $O(log n)$. And if we use a hash table such as a dictionaries in Python, we can achieve constant complexity for the search operation. So, as you can see, we reduced from a linear complexity to even constant complexity, having a good data structure. `This is why knowing which data structure to use for our problem is extremely powerful, because we can reduce the running time significantly.`

<a id='structures'></a>
# Data Structures
Modern applications manipulate large amounts of data, then _How to deal with these large amounts of data? How to make sure that the operations are going to be fast enough?_.  

`Somehow we have to make sure the application is as fast as possible and this is exactly why using the right data structures is crucial.`

The purpose of the data structures is to manage large amounts of data efficiently such as large databases, in order to boost up the running time of the algorithms. So, if we want to make sure that the given application is going to be fast enough, then we have to deal with the data structures to make sure the running complexity will be better.

It is important to remember the **tradeoff** between `time complexity` and `memory complexity`. If we want to minimize the amount of memory the given application uses, then the running time complexity is not going to be the best and the application would be slow. If we want to make sure that the application is fast so the running time complexity is the best one possible, then the memory complexity will increase which means that the application needs more memory due to the underlying data structure.

Also, it is important to notice about the underlying data structure and the abstract data type which defines the model (_logical description_) for a certain data structure. The `Abstract Data Type` does not specify the concrete implementation, but the definition of the functions the data structure will have in order to define its behavior.

For example, when we talk about a `stack abstract data type` there are three functions defined `push()`, `pop()`, and `peek()`. These functions does not define the concreate implementation, but the basic functionality to insert, remove and find items in the stack to achieve the best running time complexity. On the other hand the `stack data structure` defines the actual representation of the data, and its goal is to be able to store and retrieve data in an efficient manner, namely to be able to insert, find and remove items, ideally in $O(1)$ running time complexity.


<br>
<img src="./static/DATA-STRUCTURES TYPES.png" alt="data-structures"/>
<br><br>