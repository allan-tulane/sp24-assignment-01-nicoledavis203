

# CMPS 2200 Assignment 1

**Name:** Nicole Davis


In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} /in O(2^n)$? Why or why not? 
.  
.  Yes, 2^{n+1} is equivalent to 2*2^n, this being said, O(2^n) exists in (is <= in relation to rate of change) 2^n.
.  
.  
. 
  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     
.  
.  No, because the growth rate of 2^{2^n} is not at most porportional to O(2^n) for larger values of n. 
.  
.  
  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    
.  
.  No, because the growth rate of n^1.01 does not exist within log base 2 of n. 
.  
.  

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?  
.  
.  To exist in the Omega of log base 2 of n, n^1.01 would have to have a growth rate larger than that of log base 2 of n, which it does, so it does exist in Omega(log base 2 of n).
.  
.  
  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  
.  
.  No, because the sqrt of n grows at a faster rate than O(log base n^3) at a point. 
.  
.  
  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  
  
  No, because no value exists for C and n where the sqrt of n is greater than C * log(n)^3. 
  
  

2. **SPARC to Python** (12 pts)

Consider the following SPARC code of the Fibonacci sequence, which is the series of numbers where each number is the sum of the two preceding numbers. For example, 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610 ... 
$$
\begin{array}{l}
\mathit{foo}~x =   \\
~~~~\texttt{if}{}~~x \le 1~~\texttt{then}{}\\
~~~~~~~~x\\   
~~~~\texttt{else}\\
~~~~~~~~\texttt{let}{}~~(ra, rb) = (\mathit{foo}~(x-1))~~,~~(\mathit{foo}~(x-2))~~\texttt{in}{}\\  
~~~~~~~~~~~~ra + rb\\  
~~~~~~~~\texttt{end}{}.\\
\end{array}
$$ 

  - 2a. (6 pts) Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. (6 pts) What does this function do, in your own words?  

  The code looks at "foo" the nth number in the sequence who's position is represented by x, and if the position is 0 or 1, it returns that x value. Otherwise, if x is greater than 1, the function makes two recursive calls to itself with the arguments x-1 and x-2. The result is the sum of the values returned by these two recursive calls.

3. **Parallelism and recursion** (26 pts)

Consider the following function:  

```python
def longest_run(myarray, key)
   """
    Input:
      `myarray`: a list of ints
      `key`: an int
    Return:
      the longest continuous sequence of `key` in `myarray`
   """
```
E.g., `longest_run([2,12,12,8,12,12,12,0,12,1], 12) == 3`  
 
  - 3a. (7 pts) First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. (4 pts) What is the Work and Span of this implementation?  

Work: Total amount of computation it performs and since in this case, the work is porportional to the length of the input list, or "mylist", which iterates through each element once, making the work O(n), where n is the length of "mylist". 

Span: Span is the measure of longest chain of dependant operations, and similarly to work in this case, it would be O(n), because each iteration of the loop is independent of the other loops. They are executed in a sequential manner because there are no dependencies between the iterations. 


  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?  

Work: Porportional to the size of the input list. For each recursive level there is a constant amount of operations, there are log(n) levels of recursion. O(n log n). 

Span: Span is O(log n). 


  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  

Work: Still O(n log n)

Span: Parallelization could potentially reduce the span. If the recursive tree is perfectly balanced, the span could be reduced to O(log n), close to the depth of the recursion tree. Worst case could be O(n log n).

