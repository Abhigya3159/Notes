#### Supervised vs. unsupervised learning
- Supervised learning - goal is to predict the value of an outcome measure based on a number of input measures
- Unsupervised learning - there is no output measure; goal is to describe associations and patterns among a set of input measures

#### Learning problems
1. Classification - outcome measurement is qualitative e.g., predict whether an email is a spam, handwritten digit recognition
2. Regression - outcome measurement is quantitative e.g., predict price of stock in the future
3. Clustering - grouping data based on a set of features e.g., which genes are most similar to each other, in terms of their expression profiles across cDNA samples

#### Types of variables
1. Quantitative
2. Qualitative / Categorical / Discrete e.g., digit classes {0, 1, ..., 9}
3. Ordered Categorical e.g., {small, medium, large}

#### Representing qualitative variables
* Typically represented numerically by codes e.g, 0 = success, 1 = failure
* K-level qualitative variable - When there are more than two categories, variables are often represented by a vector of K binary variables or bits, only one of which is on at a time e.g., {0, 1, 0, 0}

#### Notation in these notes
* X = input, Y = quantitative output, G = qualitative output
* If X is a vector, its components can be accessed as X<sub>j</sub>
* *i*th observed value of X is written as x<sub>i</sub>
* Matrices e.g., a set of N input p-vectors x<sub>i</sub>, i = 1, ..., N would be represented by the N x p matrix **X**
* Training data is represented as a set of measurements (x<sub>i</sub>, y<sub>i</sub>)
* Predicted variable is represented with a subscript pred in prefix <sub>s</sub>X

#### Linear models
* Given X<sup>T</sup> = (X<sub>1</sub>, .... X<sub>p</sub>), we predict Y via the model ![Linear model]() which can be simplified to ![Simplified linear model]() by including the constant variable 1 in X and the bias/intercept B<sub>o</sub> in the vector of coefficients <sub>s</sub>B.
* If Y is a K-vector, B would be a p x K matrix of coefficients
* (X, <sub>pred</subY) represts a hyperplane in the (p+1) dimensional input/output space including the origin if the constant is included in X ![Hyperplane in 3D space]()

##### Least squares
* The most popular method of fitting a linear model to training data is least squares
* Coefficients in B are chosen so as to minimize the residual sum of squares ![Residual sum of squares]()
* The above equation can be rewritten and simplified as follows: ![RSS in matrix notation]()
* The derivation is as follows. Note w = B. The derivation makes use of the following matrix transpose and calculus properties/identities: a) X<sup>2</sup> = X<sup>T</sup>X b) (AB)<sup>T</sup> = B<sup>T</sup>A<sup>T</sup> c) ![quadratic matrix function derivative]() d) ![linear matrix function derivative]()
![Least Squares derivation]()
* y<sub>i</sub> = x<sub>i</sub><sup>T</sup>B
* The fitted values can be converted to a fitted class a follows: class A if <sub>pred</sub></sub>Y > 0.5, class B if <sub>pred</sub>Y <= 0.5
* In the case of one Gaussian per class, linear model is an almost optimal solution.
![linear plot]()

#### k-nearest-neighbours
* Find k observations closest (often measured in terms of Euclidean distance) to x<sub>i</sub> in input space and average their responses. ![k-nearest-neighbours]()
* More appropriate in the case where training data in each class comes from a mixture of low variance Guassian distributions.
![knn plot]()

#### Enhancements to LSMs and KNNs
* Kernel methods - weights that decrease smoothly to zero with distance from target point as opposed to 0/1 weights used by KNN
* Local regression - linear regression is applied to localized subsets of the data
* Neural networks - sums of non-linearly transformed linear models

#### Statistical decision theory
* The criteria used to choose f such that error between Y and f(X) is minimised is the expected (i.e, average) squared prediction error (EPE).
* Derivation
  ![regression function derivation]()
  Steps between equations 1 and 2
  ![regression function derivation continued]()
* Intuition
  ![regression function intuition]()
* Best prediction, when best is measured by average sqaure error, of Y at any point X = x is the conditional mean f(x) = E(Y|X = x).
* KNN attempts to implement the above by averaging over sample data (equivalent to expectation) and conditioning on some region 'close' to target point (approximate conditioning 'at' a point)
* As the dimension p gets large, so does the metric size of the k-nearest neighbourhood and in turn the rate of convergence of f(x) to E(Y|X = x) decreases.
* Linear regression fits into this framework on the assumption that f(x) is well approximated by a globally linear function x<sup>T</sup>B. Subs. in EPE and differentiating wrt B we get, ![Solving for B](). Derivation:
  EPE(f) = E[(Y - X<sup>T</sup>B)<sup>T</sup>(Y - X<sup>T</sup>B)]
  EPE'(f) {wrt B} = E[X(Y - X<sup>T</sup>B)] = E[XY] - E[XX<sup>T</sup>B] = 0
  E[XY] = BE[XX<sup>T</sup>]
  B = E[(XX<sup>T</sup>)]<sup>-1</sup>E(XY)
  [Refer back to least squares derivation]
* When the loss function is L<sub>1</sub>: E|Y-f(X)|, the solution is the conditional median f(x) = median(Y|X = x)
  

##### Additive model
* uses techniques such as k-nearest neighbors to approximate univariate conditional expectations simultaneously for each of the coordinate functions
  ![additive model]()

