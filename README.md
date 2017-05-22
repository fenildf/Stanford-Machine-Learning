# Stanford Machine Learning

Notes and code for Andrew Ng's class on machine learning.

## Introduction

What is Machine Learning?

Two definitions of Machine Learning are offered. Arthur Samuel described it as: "the field of study that gives computers the ability to learn without being explicitly programmed." This is an older, informal definition.

Tom Mitchell provides a more modern definition: "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

Example: playing checkers.

E = the experience of playing many games of checkers

T = the task of playing checkers.

P = the probability that the program will win the next game.

In general, any machine learning problem can be assigned to one of two broad classifications:

Supervised learning - predictive. (1) regression - predict a value we haven't seen yet (2) classification - classify something (as if into a category)

Unsupervised - find underlying structure of data. Clustering. Non-clustering - find structure in chaos, like separating voices in audio.

## Model representation

Conventions

```
m - number of training examples
x - input var / features
y - output var / target
(x, y) - training example
xi - ith training example's x
h - hypothesis function, function(x) that outputs the estimated val of y. Maps from x's to y's. example: hθ(x) = θ0 + θ1x
theta (θ) - just means an unknown that we're trying to find using ML.
```

minimize θ0 θ1 - we're minimizing the sum of squared error (see notes on [Curve Fitting](https://github.com/beatobongco/TIL/blob/master/day_notes/2017-05-04_Curve_Fitting.md)) / 2m.

J(θ0, θ1) - squared error cost function, used to measure the accuracy of our hypothesis function

Why do we square errors? Most commonly used one for regression problems.

The mean is halved as a convenience for the computation of the gradient descent, as the derivative term of the square function will cancel out the term.

## Gradient descent

![image](https://cloud.githubusercontent.com/assets/3739702/26201119/f4e4503a-3c03-11e7-8c58-90994d4e7f07.png)

:= is an assignment operator

α or alpha is the learning rate. Think of it as how big the steps are

The gradient descent algorithm simultaneously updates theta values (store vals in temp variables

The derivative part of the algo works by finding the slope of the line tangent to the point.

Then we subtract learning rate * slope from theta. This is to get to the minimum. If you look at the graph, slope is positive so theta - positive number means we go down.

![image](https://cloud.githubusercontent.com/assets/3739702/26201132/09473e98-3c04-11e7-856e-b922fdfb93ca.png)

If learning rate is too small, gradient descent will be slow. If too big can overshoot or diverge.

### Gradient descent algorithm expanded

![image](https://cloud.githubusercontent.com/assets/3739702/26201818/6564fff0-3c07-11e7-9324-acc6ea600cdb.png)

Gradient descent works because there's no local optima, just one global optimum.

## Linear Algebra review

Recall syntax of Aij = i, j enrtry, ith row jth column. R can be used to denote matrices. e.g. R3x3

Vector - 1 col matrix. n-dimensional vector. e.g. R4

Convention: uppercase for matrices and lowercase for vector.

Adding matrices: just add elements in same place. Can only add matrices with same dimension.

Scalar multiplication/division: just multiply/divide the scalar with each element in matrix.

MDAS applies to matrix operations.

### Multiplying matrices and vectors

![image](https://cloud.githubusercontent.com/assets/3739702/26272529/5ce8e50c-3d4d-11e7-9db2-0424254b3157.png)

Just multiply each row element of the matrix by its corresponding element of the vector and sum them. This sum is the first element of the new vector.

The resulting vector length will be equal to the column length of the matrix.

You can only multiply matrices and vectors of same size (matrix row size and vector size)

### Why is this useful?

You can use matrix vector multiplication to get predictions given a hypothesis.

![image](https://cloud.githubusercontent.com/assets/3739702/26272604/453b6360-3d4f-11e7-9738-5bf07d2a6258.png)

Doing it this way (in any programming language) is more efficient than implementing a `for` loop.

### Matrix x matrix

Simple as repeated matrix vector multiplication.

![image](https://cloud.githubusercontent.com/assets/3739702/26272795/2d0a6520-3d54-11e7-9225-36313f247bfa.png)

Some rules:

![image](https://cloud.githubusercontent.com/assets/3739702/26272807/93065078-3d54-11e7-9168-cf530ea41298.png)

This is useful for applying multiple hypotheses to your data.

![image](https://cloud.githubusercontent.com/assets/3739702/26272861/93efc3ec-3d55-11e7-976b-bb0e27d491ef.png)

### Properties of matrices

1. Not commutative.

`A x B != B x A`

2. Is associative.

`A x B x C === A x (B x C) === (A x B) x C`

3. Identity matrix

![image](https://cloud.githubusercontent.com/assets/3739702/26272922/daf3f41a-3d56-11e7-85bd-47a42486b613.png)

### Matrix Inverse

Inverse is basically A * Inverse = Identity matrix

![image](https://cloud.githubusercontent.com/assets/3739702/26291146/581d14ee-3ee7-11e7-89ce-49722821fa85.png)

Not all matrices have inverse, these are called "singular" or "degenerate".

### Matrix Transpose

![image](https://cloud.githubusercontent.com/assets/3739702/26291334/846deb9e-3ee8-11e7-9e03-0aefc4676c5f.png)

## Multivariate Linear Regression

Recall:

![image](https://cloud.githubusercontent.com/assets/3739702/26306140/364c9eb6-3f2d-11e7-8ee1-9867fd886057.png)

We are setting x sub 0 to 1 for convenience purposes. This is so we can perform matrix operations on theta and x. Also because of this, hypothesis can now be written as theta transpose x.

### Feature scaling

If features are on different scale, it will take long time to converge to global minimum.

Solution is to scale features.

e.g. You have 2 features, number of rooms (1-5) and size in sq ft (0 - 2000) it can make your contour graph look funky. Solution is to divide no. of rooms / 5 and size / 2000 to make them be between 0 and 1.

Feature scaling generally is getting every feature into approx: `-1 <= xi <= 1`

Some features that are not too huge are OK to leave alone though (-/+ 3 and -/+ 1/3)

### Mean normalization

![image](https://cloud.githubusercontent.com/assets/3739702/26308039/7189b694-3f32-11e7-8dff-f168559c3d27.png)

### Features and Polynomial Regression

To improve features...

* you can combine multiple features in to one (e.g. width x height)
* change curve of the hypothesis function by making it quadratic, cubic, etc. Note that scaling becomes more important if you use this.



