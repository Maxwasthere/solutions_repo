# Estimating π using Monte Carlo Methods

## Estimating π Using a Circle

### Theoretical Foundation

To estimate the value of π using a Monte Carlo method, we use the relationship between the area of a circle and the area of the square that bounds it.

Consider a unit circle (radius $r = 1$) inscribed in a square with side length 2. The circle is centered at the origin, and the square spans from $-1$ to $1$ along both the x and y axes.

- The **area of the circle** is: 

  $A_{\text{circle}} = π \cdot r^2 = π$


- The **area of the square** is:  

  $A_{\text{square}} = (2 \cdot r)^2 = 4$

If we randomly generate a large number of points uniformly distributed across the square, the **ratio of points that fall inside the circle to the total number of points** will approximate the ratio of their areas:

$$
\frac{\text{points inside circle}}{\text{total points}} \approx \frac{A_{\text{circle}}}{A_{\text{square}}} = \frac{π}{4}
$$

Rearranging this gives the formula for estimating π:

$$
π \approx 4 \cdot \left(\frac{\text{points inside the circle}}{\text{total points}}\right)
$$

This approach works because, as the number of points increases, the distribution of points becomes more uniform, and the estimate converges toward the true value of π.

---

### Simulation

To estimate π using this method, I simulated the process by generating random points inside a square and checking whether each point falls inside the inscribed unit circle.

Here’s how the simulation works:

- Generate $N$ random points $(x, y)$ where both $x$ and $y$ are uniformly distributed between $-1$ and $1$.

- For each point, check whether it lies inside the unit circle using the inequality:  
  $x^2 + y^2 \leq 1$


- Count how many points satisfy this condition.

- Estimate π using the formula:


  $π \approx 4 \cdot \left(\frac{\text{points inside circle}}{\text{total points}}\right)$
