# Generating a Uniform Distribution of Points on an Ellipsoid

This repository includes code to generate a uniform distribution of points on the surface of an ellipsoid with axes `a`, `b`, and `c`. The approach, based on this [Stack Exchange post](https://math.stackexchange.com/questions/973101/how-to-generate-points-uniformly-distributed-on-the-surface-of-an-ellipsoid), is outlined below.

### Steps to Generate Points

1. **Generate Points on a Sphere**  
   Choose a point $(x,y,z)$ uniformly on a sphere by sampling 3 points on a multivariate standard normal distribution on $\mathbb{R}^3$. For more details, refer to this [explanation on Cory Simon's blog](https://corysimon.github.io/articles/uniformdistn-on-sphere/).

2. **Map to the Ellipsoid**  
   To transform the points from the unit sphere to the ellipsoid, apply the mapping:
   
   $f(x, y, z) \rightarrow (x' = ax, y' = by, z' = cz)$

3. **Correct for Distortion**  
   To correct the distortion introduced by scaling, discard points with a probability $p(x, y, z) = \frac{\mu_{(x, y, z)}}{\mu_{\text{max}}}$, where:

   $\mu_{(x, y, z)} = \sqrt{(acy)^2 + (abz)^2 + (bcx)^2}$

   The script sets $\mu_{\text{max}} = ab$, corresponding to a maximum radius at `(0, ±1, 0)` on the ellipsoid.
