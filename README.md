# DDL
The goal of DDL is to implement the Doubly Debiased Lasso estimator proposed in  <https://arxiv.org/abs/2004.03758>. It Computes the Doubly Debiased Lasso estimator of a single regression coefficient in the high-dimensional linear model with hidden confounders and also constructs the confidence interval forthe target regression coefficient.

## Installation 
You can install the released version of DDL from CRAN with:
```R
install.packages("DDL")
```
## Example
This is a basic example which shows you how to solve a common problem
```R
idx=1
n=2000
p=200
s=5
q=3
sigmaE=2
sigma=2
pert=1

H = pert*matrix(rnorm(n*q,mean=0,sd=1),n,q,byrow = TRUE)
Gamma = matrix(rnorm(q*p,mean=0,sd=1),q,p,byrow = TRUE)
#value of X independent from H
E = matrix(rnorm(n*p,mean=0,sd=sigmaE),n,p,byrow = TRUE)

#defined in eq. (2), high-dimensional measured covariates
X = E + H %*% Gamma

delta = matrix(rnorm(q*1,mean=0,sd=1),q,1,byrow = TRUE)

#px1 matrix, creates beta with 1s in the first s entries and the remaining p-s as 0s
beta = matrix(rep(c(1,0),times = c(s,p-s)),p,1,byrow = TRUE)

#nx1 matrix with values of mean 0 and SD of sigma, error in Y independent of X
nu = matrix(rnorm(n*1,mean=0,sd=sigma),n,1,byrow = TRUE)

#eq. (1), the response of the Structural Equation Model
Y = X %*% beta + H %*% delta + nu

DDL(X,Y,idx)
```
