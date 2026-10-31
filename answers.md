# CMPS 2200 Assignment 4
## Answers

**Name:**_________________________

Place all written answers from `assignment-04.md` here for easier grading.


**1 Quicksort probabilities**

- **1a. (5 pts)** What is the probability that Quicksort does $\Omega({n^2})$ comparisons? 
Let X be the number of comparisons Quicksort makes. We know
E[X] = O(n log n), so E[X] ≤ k·n lg n for some constant k. Setting α = c·n²

P[X ≥ c·n²] ≤ (k·n lg n) / (c·n²) = O(lg n / n)

That goes to 0 as n gets bigger, so Quicksort doing Ω(n²) comparisons becomes less likely for bigger inputs.


- **1b. (5 pts)** What is the probability that Quicksort does $10^c n \lg n$
comparisons, for a given $c>0$? What does this say about the
deviation of the actual work from the expected work for Quicksort?

Set α = 10^c · n lg n and use E[X] ≈ n lg n:

P[X ≥ 10^c · n lg n] ≤ (n lg n) / (10^c · n lg n) = 10^(−c)

So the chance of doing 10× more work than expected is at most 1/10, 100× more is at most 1/100, and so on. The probability drops off exponentially in c, so the actual work is very unlikely to be much worse than the expected O(n lg n).



**2 From "Maybe" to "Definitely"**

- **2a. (10 pts)** Give an algorithm to improve the guaranteed success probability and state its work.




- **2b. (6 pts)** Show how to convert $\mathcal{A}$ into an
  algorithm that always produces the correct result, but has an
  expected runtime that depends on $w(n)$ and a success probability
  $\epsilon$.

**3 Determinism versus Randomization in Quicksort**


- **3b. (8 pts)** Compare running times using `compare-qsort` between variants of Quicksort and the provided implementation of selection sort (`ssort`).
Sorted input:
|   n |   ssort |   qsort-fixed-pivot |   qsort-random-pivot |
|-----|---------|---------------------|----------------------|
| 100 |   0.192 |               0.690 |                0.195 |
| 200 |   0.682 |               2.280 |                0.375 |
| 400 |   2.600 |               8.709 |                0.787 |
| 800 |   9.926 |              31.788 |                1.772 |

Random input:
|   n |   ssort |   qsort-fixed-pivot |   qsort-random-pivot |
|-----|---------|---------------------|----------------------|
| 100 |   0.231 |               0.183 |                0.184 |
| 200 |   0.830 |               0.344 |                0.401 |
| 400 |   3.109 |               0.701 |                0.864 |
| 800 |  12.104 |               1.517 |                1.856 |

The times match the theory. When n doubles, selection sort gets about 4x slower (n²) and quicksort gets about 2x slower (n log n).

On random input, both quicksorts are about 7x faster than selection sort at n = 800 and perform about the same as each other.

On sorted input, fixed pivot quicksort becomes n² because the first element is always the smallest, so each call only removes one element. It ended up slower than selection sort (31.8 ms vs 9.9 ms). Random pivot quicksort ran about the same on both inputs, since a random pivot can't be forced into the worst case.


- **3c. (8 pts)** Compare the fastest of your sorting implementations to the Python sorting function `sorted`, conducting the tests in 3b above. 
