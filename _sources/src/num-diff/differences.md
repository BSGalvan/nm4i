# Forward, Backward, Central Differences

## Getting Started

The concept of numerical differentiation is tied to the concept of the limit of a
function. Recall that for a continuous function $f(x)$, the value of the first
derivative at a point $x = x_0$ is given by:

$$
    f^′(x_0) = \lim_{h → 0} \dfrac{f(x_0 + h) - f(x_0)}{h}
$$

if this limit exists. Equivalently, we can write this limit as:

$$
    f^′(x_0) = \lim_{h → 0} \dfrac{f(x_0) - f(x_0 - h)}{h}
$$

By the very fact that the function is continuous, these two limits (should they exist)
will be equal. In the realm of mathematics, $h$ can be made as small as possible in
order to compute the derivative, which is unfortunately a task too tedious for computers
to handle.

Thus, in order to compute these limits (and by extension the derivative of
the function) numerically, we notice that the above equations can be written as:

$$
    f^′(x_0) ≈ \dfrac{f(x_0 + Δx) - f(x_0)}{Δx}
$$

and 

$$
    f^′(x_0) ≈ \dfrac{f(x_0) - f(x_0 - Δx)}{Δx}
$$

The former equation is known as the **forward difference**, whereas the latter is the
**backward difference** equation for the numerical derivative. One can see that these two
expressions will approximate the derivative quite well, but to actually estimate the
error, we use the Taylor expansion of the function around $ x = x_0$:

$$
    f(x_0 + Δx) = f(x_0) + Δx f^′(x_0) + \dfrac{Δx^2}{2} f^{\prime \prime}(x_0) + …
$$

Rearranging this gives us the following:

$$
    f^′(x_0) ≈ \dfrac{f(x_0 + Δx) - f(x_0)}{Δx} - O(Δx)
$$

which shows that the approximation is first-order accurate. A similar result can be
derived for the backward difference equation as well.

## Doing Better

However, in most cases, first-order accuracy is much too error-prone, unless you reduce
$Δx$ to miniscule values. Thus, we must do better than this and the way we start is
by asking what happens when we combine the forward and backward differences ...

$$
    \begin{equation}
        2 \cdot f^′(x_0) ≈ \dfrac{f(x_0 + Δx) - f(x_0 - Δx)}{Δx}
        ⇒ f^′(x_0) ≈ \dfrac{f(x_0 + Δx) - f(x_0 - Δx)}{2 Δx}
    \end{equation}
$$

The result of this combination is that the approximation so produced is _second-order
accurate_ (this can be checked by using Taylor expansions, as before). This form of the
first derivative is known as the **central difference**.

Notice that when comparing the forward/backward and central differences, the former has
=======
one less function evaluation than the latter (since usually $f(x_0)$ is a known
quantity). This is true in general as well, wherein methods with a higher number of
functional evaluations will exhibit higher-order accuracy (once these evaluations are
weighted properly).
