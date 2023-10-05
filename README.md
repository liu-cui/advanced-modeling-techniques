# Modeling
advanced modeling techniques

## Overview 
Overview of selectd modeling techniques
- Range constraints
- Special functions: absolute value, piecewise linear, min/max
- Logical conditions on binary variables
- Logical conditions on constraints
- Semi-conditinous variables
- Selecting big-M values

some popular logical expressions:
- Absolute value
- Min/Max value
- And/Or over binary variables
- Indicator(if-then logic)

# Range constraints
Many models contain constraints like: $L \leq \sum_{i}a_{i}x_{i} \leq U$

These can be rewritten as: 
$ r + \sum_{i}a_{i}x_{i}=U $

$ 0 \leq r \leq U-L$

# Absolute value

### Convex case
Simply substitute if absolute value function creates a convex model: $\min\|x\|$

$\min z$ \
$z = x_p + x_n$ \
$x = x_p - x_n$ 

### Non-convex case
Use indicator variable and arbitrary big-M value to prevent both $x_p$ and $x_n$ positive: $max\|x\|$

$max z$ \
$z = x_p + x_n$ \
$x = x_p - x_n$ \
$x_p \leq My$ \
$x_n \leq M(1-y)$ \
$y\in \{0,1\}$ 


### Sepcial Ordered Sets（特殊顺序集）
- Specical Ordered Sets of type 1 (SOS-1) : at most one variable in set may be no-zero
- Specical Ordered Sets of type 1 (SOS-2) : an ordered set where
  - at most two variable in set may be no-zero
  - non-zero variable must be adjacent(近邻的)
- Variables need not be integer

### SOS-1 constraint 
Use SOS-1 constraint to prevent both $x_p$ and $x_n$ positive: $max\|x\|$

$max z$ \
$z = x_p + x_n$ \
$x = x_p - x_n$ \
$x_p, x_n \in SOS-1$ 

- No big-M value needed
- Works for both convex and non-convex version

>Which will perform better?

### SOS constraints vs big-M representation

- SOS constraints are handled with branching rules(not included in LP relaxation)
- SOS advantages:
  - always valid(no reasonable M in some cases)
  - numerically stable
- Big-M advantages:
  - LP relaxation is tighter
  - typically results in better performance as long as M is relatively small


# Piecewise linear functions

Generalization of absolute value functions

Convex case is easy
- Function represented by LP

Non-convex case is more challenging 
- Function represented as MIP or SOS-2 constraints

### Piecewise linear functions - Applications

- Piecewise linear functions appear in models all the time
- Examples:
  - Fixed costs in manufacturing due to setup
  - Economies of scale when discounts are applied after buying a certain number of items
- Also useful when approximating non-linear functions
  - More pieces provide for a better approximation
- Examples:
  - Unit commitment models in energy sector
  - ...
 
     
### Piecewise linear functions - SOS-2 constraint

![截屏2023-10-05 18 41 06](https://github.com/liu-cui/advanced-modeling-techniques/assets/55623869/45b14927-e326-4938-9023-acf623af45da)

- Let $(x_i,y_i)$ represent $i^{th}$ point in piecewise linear function
- To represent $y=f(x)$, use: $x=\sum_i\lambda_ix_i$

$y=\sum_i\lambda_iy_i$ \
$\sum_i\lambda_i = 1$ \ 
$\lambda_i\geq 0, SOS-2$

- SOS-2 constraint is redundant if $f$ is convex
- Binary representation also exists

# Min/max functions - Convex case
- Easy to minimize the largest value (minimax) or maximize the smallest value (maximin)

$min\{max_i x_i\}$  can be rewritten as: 

$min z$ \
$z\geq x_i \forall i$










  



