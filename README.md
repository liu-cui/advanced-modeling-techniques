


# Table of Content

advanced modeling techniques

* [Overview](#overview)
* [Range Constraints](#range_constraints)
* [Absolute Value](#absolute_value)
  * [Convex Case](#convex_case)
  * [Non-convex Case](#non-convex_case)
* [Sepcial Ordered Sets: SOS](#sepcial_ordered_sets)
  * [SOS1 Constraint](#sos1_constraint)
  * [SOS Constraints VS bigM Representation](#sos_constraints_vs_bigm_representation)
* [Piecewise Linear Functions](#piecewise_linear_functions)
  * [Piecewise Linear Functions Applications](#piecewise_linear_functions_applications)
  * [Piecewise Linear Functions SOS2 Constraint](#piecewise_linear_functions_sos2_constraint)
* [Min/Max Functions](#min_max_functions)
  * [Non-convex Case](#non-convex_case)
  * [Convex Case](#convex_case)
* [Logical Conditions On Binary Variables](#logical_conditions_on_binary_variables)
* [Logical Conditions Variable Result](#logical_conditions_variable_result)
* [Logical Conditions On Inequalities Or](#logical_conditions_on_inequalities_or)
* [Logical Conditions On Equalities Or](#logical_conditions_on_equalities_or)


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

## Range_Constraints
Many models contain constraints like: $L \leq \sum_{i}a_{i}x_{i} \leq U$

These can be rewritten as: 
$$r + \sum_{i}a_{i}x_{i}=U $$
$$0 \leq r \leq U-L$$

## Absolute_Value

### Convex_Case
Simply substitute if absolute value function creates a convex model: $\min\|x\|$
$$\min z$$
$$z = x_p + x_n$$
$$x = x_p - x_n$$

### Non-convex_Case
Use indicator variable and arbitrary big-M value to prevent both $x_p$ and $x_n$ positive: $\max\|x\|$

$$\max z$$
$$z = x_p + x_n$$
$$x = x_p - x_n$$
$$x_p \leq My$$
$$x_n \leq M(1-y)$$
$$y\in \\{0,1\\}$$ 


## Sepcial_Ordered_Sets

- Specical Ordered Sets of type 1 (SOS-1) : at most one variable in set may be no-zero
- Specical Ordered Sets of type 1 (SOS-2) : an ordered set where
  - at most two variable in set may be no-zero
  - non-zero variable must be adjacent(近邻的)
- Variables need not be integer

### SOS1_Constraint 
Use SOS-1 constraint to prevent both $x_p$ and $x_n$ positive: $\max\|x\|$
$$\max z$$
$$z = x_p + x_n$$
$$x = x_p - x_n$$
$$x_p, x_n \in SOS-1$$ 

- No big-M value needed
- Works for both convex and non-convex version

>Which will perform better?

### SOS_Constraints_VS_bigM_Representation

- SOS constraints are handled with branching rules(not included in LP relaxation)
- SOS advantages:
  - always valid(no reasonable M in some cases)
  - numerically stable
- Big-M advantages:
  - LP relaxation is tighter
  - typically results in better performance as long as M is relatively small


## Piecewise_Linear_Functions

Generalization of absolute value functions

Convex case is easy
- Function represented by LP

Non-convex case is more challenging 
- Function represented as MIP or SOS2 constraints

### Piecewise_Linear_Functions_Applications

- Piecewise linear functions appear in models all the time
- Examples:
  - Fixed costs in manufacturing due to setup
  - Economies of scale when discounts are applied after buying a certain number of items
- Also useful when approximating non-linear functions
  - More pieces provide for a better approximation
- Examples:
  - Unit commitment models in energy sector
  - ...
 
     
### Piecewise_Linear_Functions_SOS2_Constraint

![截屏2023-10-05 18 41 06](https://github.com/liu-cui/advanced-modeling-techniques/assets/55623869/45b14927-e326-4938-9023-acf623af45da)

- Let $(x_i,y_i)$ represent $i^{th}$ point in piecewise linear function
- To represent $y=f(x)$, use:
$$x=\sum_i\lambda_ix_i$$
$$y=\sum_i\lambda_iy_i$$
$$\sum_i\lambda_i = 1$$
$$\lambda_i\geq 0$$
$$SOS2$$
- SOS2 constraint is redundant if $f$ is convex
- Binary representation also exists

## Min_Max_Functions
### Non-convex_case
- Easy to minimize the largest value (minimax) or maximize the smallest value (maximin)

$\min\\{\max_i x_i\\}$  can be rewritten as: 
$$\min z$$
$$z\geq x_i \forall i$$

### Convex_case
- Harder to minimize the smallest value (minimin) or maximize the largest value (maximax)
  - Use multiple indicator variables and big-M value

- $\min \\{\min_{i} x_{i} \\}$ can be rewritten as:
$$\min z$$
$$z \geq x_i - M(1-y_i)$$
$$\sum_iy_i=1$$
$$y_i \in \\{0,1\\}$$

## Logical_Conditions_On_Binary_Variables

- **And**
  - $x_1 = 1$ and $x_2 = 1$
  - $x_1 + x_2 = 2$
- **Or**
  - $x_1 = 1$ or $x_2 = 1$
  - $x_1 + x_2 \geq 1$
- **Exclusive or (not both)**
  - $x_1 = 1$ xor $x_2 = 1$
  - $x_1 + x_2 = 1$
- **At least / at most / counting**
  - $x_i = 1$ for at least 3 $i^{'}$s
  - $\sum_{i}x_i \geq 3$
- **If-then**
  - if $x_1=1$, then $x_2=1$
  - $x_1 \leq x_2$
 
## Logical_Conditions_Variable_Result

- **And**
  - $y = (x_1$ and $x_2=1)$
$$y\leq x_1$$ 
$$y\leq x_2$$ 
$$y\geq x_1 + x_2 -1$$

- **Or**
  - $y = (x_1$ or $x_2=1)$
$$y\geq x_1$$ 
$$y\geq x_2$$ 
$$y\leq x_1 + x_2$$

- **Exclusive or (not both)**
  - $y = (x_1$ xor $x_2=1)$
$$y\geq x_1 - x_2$$ 
$$y\geq x_2 - x_1$$
$$y\leq x_1 + x_2$$
$$y\leq 2 - x_1 - x_2$$


## Logical_Conditions_On_Inequalities_Or

- Use indicator for the satisfied constraint, plus big-M value

$\sum_{i}a_i^{1}x_{i} \leq b^1$   or  $\sum_{i}a_i^{2}x_{i} \leq b^2$  or  $\sum_{i}a_i^{3}x_{i} \leq b^3$

rewritten as: 

$$\sum_{i}a_i^{1}x_{i} \leq b^1 + M(1-y^{1})$$ 
$$\sum_{i}a_i^{2}x_{i} \leq b^2 + M(1-y^{2})$$ 
$$\sum_{i}a_i^{3}x_{i} \leq b^3 + M(1-y^{3})$$ 
$$y^{1} + y^{2} + y^{3} \geq 1$$ 
$$y^{1}, y^{2}, y^{3} \in \\{0, 1\\}$$ 

## Logical_Conditions_On_Equalities_Or

- Add a free slack variable to each equality constraint
- Use indicator variable to designate whether slack is zero

$$\sum_{i}a_{i}^{k}x_{i}  = b^{k}$$

rewritten as: 

$$\sum_{i}a_{i}^{k}x_{i} + w^{k} = b^{k}$$
$$w^{k} \leq M(1-y^{k})$$
$$w^{k} \geq -M(1-y^{k})$$
$$y^{k}\in \\{0, 1\\}$$














  



