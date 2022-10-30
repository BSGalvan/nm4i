# Bisection Method

The bisection method is one of the simplest root-finding methods around. Owing to its
simplicity, it is guaranteed to eventually converge, given that the initial problem
satisfies certain conditions. However, it also is one of the _slowest_ converging
algorithms due to its relatively mild assumptions.
It is a good method to try if you want to approximate the root quickly, but then
refinement of that root is best done using another root-finding routine.

## Conditions for the Initial Problem

For bisection to work, it is necessary that the function for which we want the root has
the following properties:

- The function is continuous.
- There are two values of inputs, say \\(a\\) and \\(b\\), for which we know that \\(
  f(a) \cdot f(b) < 0 \\)

From these two conditions, using the [Intermediate Value
Theorem](https://en.wikipedia.org/wiki/Intermediate_value_theorem), we see that the
interval \\((a, b)\\) must 'bracket' the root that we require.

## Motivating the Algorithm

At this point, we know that the root (call it \\(x_0\\)) lies _somewhere_ in the
interval \\((a, b)\\). What we would like to do is to successively shrink this interval
till we have found the root. The way we shrink the interval is as follows:

1. Calculate the midpoint of the interval, \\(c\\).
2. Calculate \\(f(c)\\).
3. If convergence is satisfactory (i.e if \\(c - a\\) or \\(|f(c)|\\) is sufficiently
   small), output c and stop.
4. If not, examine the sign of \\(f(c)\\) and replace either \\((a, f(a))\\) or \\((b,
   f(b))\\) with \\((c, f(c))\\) so that there is a zero crossing in the new interval
   and repeat.

Ideally, this process can go on infinitely but on a computer, we will eventually hit
what is called the [machine epsilon](https://en.wikipedia.org/wiki/Machine_epsilon),
\\(\epsilon\\). The machine epsilon is inherently tied to the fact that computers have
finite precision, meaning that computers can only store up to a fixed number of
significant digits. The result of this is that any two numbers which differ by _less_
than the machine epsilon will _not_ be distinguishable by the computer. This forms the
basis for the exit condition in Step 3 above, but more elaborate conditions are also
used in more complex situations.

In practice we usually do not desire a precision which is of the order of
\\(\epsilon\\), and can tolerate a much higher error. In this case, we simply check if
\\(|c-a|\\) or \\(|f(c)|\\) are smaller than some supplied tolerance value and if true,
we stop the process. In addition to this provision, it may so happen that the function
converges so slowly that the algorithm doesn't reach a precision level that we desire.
In these cases, we supply an additional parameter called \\(N_{max}\\) which is the
maximum number of iterations to carry out, before the main loop body quits.

## The Algorithm in Code

The following is a Python snippet illustrating an example implementation of the
bisection method. Here, `f` is the function we need to find the root for, `a` and `b`
are the endpoints of the interval such that `a < b`, and `N_MAX` is a constant
for the maximum number of iterations to undertake.

```python
for iter in range(N_MAX):                  # limit iterations
    c = (a + b) / 2                        # new midpoint
    if f(c) = 0 or (b - a)/2 < TOL         # exit condition
        print(f"Solution found, x = {c}")  # output c
        break                              # stop iterating
    iter += 1
    if f(c) * f(a) > 0 a = c else b = c    # step 4, written differently
```

## Epilogue

As we've seen above, the bisection method is quite simple in its implementation and
concept, and works for a wide-variety of functions. However, it can be shown that it
converges _linearly_, which is extremely slow if one requires high precision. We use the
bisection method at all because it is the only method which guarantees an estimate that,
in the worst-case, will have an absolute error given by the tolerance in the _least_
number of iterations when compared to other algorithms.

That being said, we will see other methods in this chapter which trade off worst-case
performance for orders-of-magnitude speedup in convergence to the root.
