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

## Range constraints
Many models contain constraints like: $L \leq \sum_{i}a_{i}x_{i} \leq U$

These can be rewritten as: 
$ r + \sum_{i}a_{i}x_{i}=U $

$ 0 \leq r \leq U-L$

## Absolute value

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

### SOS-1 constraint 
Use SOS-1 constraint to prevent both $x_p$ and $x_n$ positive: $max\|x\|$

$max z$ \
$z = x_p + x_n$ \
$x = x_p - x_n$ \
$x_p, x_n \in SOS-1$ 

- No big-M value needed
- Works for both convex and non-convex version

>Which will perform better?









  



