# Lab 4: Concept Review

This lab reviews the foundational concepts of algorithms and data structures that we have covered in the first half of the course. 

**Instructions:** To complete this lab, you may work in groups, but you must write your solutions yourself. Choose two of the topics below that you need to review and complete the corresponding problems. Where relevant, you are given the answer and must provide the justification as your solution. Once you have completed the lab, push your changes to your forked repository.

**Topics:** asymptotic analysis, data structures, empirical comparison of algorithms, pseudocode, greedy algorithms. 

## Asymptotic Analysis

1. Use the rules from lecture 07 to prove that $T(n) = 5 \log n + 7n$ is $\mathcal{O}(n)$.

By the dropping constants property, $T(n) = \log n + n$.
Then, by the sum is max property, $T(n) = n$.
So, ${O}(n) = n$.

2. True/False/Possibly: $T(n)$ is $\mathcal{O}(n^2)$?

**Answer**: Yes

**Justification**: This is possible because 

3. True/False/Possibly: $T(n)$ is $\Omega(n \log n)$?

**Answer**: No

**Justification**:

4. For any algorithm, we can give a trivial lower bound. What is that lower bound?

**Answer**: $\Omega(1)$

**Justification**:

5. Is there a corresponding trivial upper bound? Why or why not?

**Answer**: No

**Justification**:


## Data Structures

1. You are programming a robot to navigate a maze. As the robot moves forward, it records each intersection it passes. When it hits a dead end, it needs to retreat to the most recently visited intersection to try a different path.

**Answer**: Stack

**Justification**: LIFO (last in first out). The stack would be the best data structure to use because the robot will need to remove the most recent record when completing the maze.

2. A server receives a massive influx of data packets from a streaming video application. To prevent the video from skipping or playing out of order on the user's end, the server must process and forward these packets in the exact sequence they were received.

**Answer**: Queue

**Justification**: FIFO (first in first out). The queue would be the best data structure to use because the server must process and forward the packets in the same sequence they were received. Since we want them to go out in the same sequence they came in, a queue would be best. 

3. An atmospheric monitoring system reads temperature data from 10,000 sequentially numbered sensors (IDs 0 through 9999). Throughout the day, the system needs to constantly update and read the current temperature of randomly selected sensors based on their ID number to build localized weather maps.

**Answer**: Array

**Justification**: An array is best because the data is sequentially numbered and indexed. An array allows the data is be indexed with the head randomly jumping around.

4. You are building a lightweight syntax checker for a code editor. Its sole job is to scan a document and ensure that every opened parenthesis `(`, bracket `[`, and brace `{` is matched with its corresponding closing character in the correct nested order.

**Answer**: Stack

**Justification**: LIFO (last in first out). Since parentheses, brackets, and braces would look like this: `( [ { } ] )`, we want to use the stack where it removes the first found of these characters. Since every one of them needs to be closed, it would scan an open character and then keep checking for the closed character, unless another open character is introduced, where it would then switch to checking for the new open character's closed character.

## Empirical Comparison of Algorithms

1. A student is benchmarking an algorithm that takes a list as its input. They run it on progressively larger randomly generated lists, doubling the number of elements ($n$) and record the following execution times:

- $n = 1000$: 0.12 seconds
- $n = 2000$: 0.94 seconds
- $n = 4000$: 7.61 seconds
- $n = 8000$: 60.85 seconds

 Based on this empirical data, what is the most likely asymptotic time complexity of the algorithm? **Hint**: Calculate the doubling ratio between each pair of consecutive runs.

 **Answer**: Cubic time complexity, $\mathcal{O}(n^3)$

**Justification**: Since $\mathcal 0.94 / 0.12$ = 7.83, 7.61 / 0.94 = 8.10, and 60.85 / 7.61 = 8.00, we will average the doubling ratio to 8.00. Next, we'll solve $\mathcal \log 2(8)$ which gives us 3. So, this algorithm has $\mathcal{O}(n^3)$ or cubic time complexity.

 2. Two students write separate algorithms to compute a metric over an array of 10 million integers. Both algorithms perform exactly one mathematical operation per element, meaning both have a theoretical time complexity of $O(N)$. However, during benchmarking, Algorithm A consistently runs 15x faster than Algorithm B. Why might theoretical Big-O analysis fail to predict this massive performance gap? 

**Answer**: Big-O analysis might fail to predict this massive performance gap because of the dropping constants property. Since both algorithms are running at ${O}(N)$ time complexity, Algorithm B could be running at $\mathcal O(15N)$. This would make Algorithm A, if running at ${O}(N)$ time complexity, run 15x faster than Algorithm B.

 3. Scenario: To measure the running time of algorithms for an empirical comparison, a developer writes the following benchmarking script:

```python
import time

large_array = [i for i in range(1000000)] [1,2,3,4,5,6,7,]
start = time.time()
myAlg(large_array)
end = time.time()

print("Time:", end - start)
```

They run this script exactly once for each algorithm on their laptop while streaming a movie in the background. Identify at least three distinct methodological flaws in this benchmarking setup that make the results unreliable.

**Answer**: One problem is that they are running this script only once. They should probably run it 5-10 times and take the average of each time collected. Another problem is that they are streaming a movie in the background, which could interfere with experiment because of how their CPU is being distributed. A third problem is that the input list should have random values inside of it, or the length of the list should be random. This is so we can cover more ground, and for real world applications, the data won't be in sequential order. 

## Pseudocode

1. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
count = 0
for i = 1 to N do
    for j = i to N do
        do_work()
```

Write a closed-form expression for the number of times `do_work()` is called in terms of $N$.
1,2,3,...,n
2,3,4,...,n
3,4,5,...,n
n + n-1 + n-2 + n-3

1,1,1
1,1
1
= 6
3^2 - 3 = 6

Closed-form expression for the number of times `do_work()` is called: n^2 - n

2. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
i = N
while i > 0:
    for j = 1 to i:
        do_work()
    i = floor(i / 2)
```

If $N=16$, how many times is `do_work()` called?

**Answer**: 31

**Justification**:

## Greedy Algorithms

You are organizing a film festival but only have access to a single screen. You are given a list of $n$ films, each with a specific `start_time` and `end_time`. You want to screen the maximum number of films possible.

Consider the following three greedy strategies:

- **Shortest First**: Always pick the film with the shortest duration (that doesn't conflict with already chosen films).
- **Earliest Start**: Always pick the film that starts the earliest (that doesn't conflict).
- **Earliest Finish**: Always pick the film that finishes the earliest (that doesn't conflict).

Which of these three strategies guarantees an optimal solution (maximum number of films)? For the two strategies that fail, provide a counter-example (a small set of film times) where the greedy choice results in a sub-optimal schedule.

**Answer**: The earliest finish strategy guarantees an optimal solution.

**Justification**: