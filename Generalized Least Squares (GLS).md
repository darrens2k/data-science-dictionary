# Generalized Least Squares (GLS)

Credits: ChatGPT, Investopedia

### What is it?

This is a regression method similar to [OLS](Ordinary%20Least%20Squares%20Regression%20(OLS).md).

### What do we use it for?

This is often used in [Linear Regression](Linear%20Regression.md) to determine the values of the coefficients when certain conditions of [OLS](Ordinary%20Least%20Squares%20Regression%20(OLS).md) are not met. Namely correlation within the error terms (auto correlation), or the variance of the error terms are unequal (heteroscedasticity). 

### How does it work?

I will only explain this method for the case of multiple linear regression with a matrix representation, however, this method can be extended to simple linear regression. It is worth noting that it would be quite rare to need to apply GLS to simple linear regression.

The regression equation we begin with: $$\begin{equation}Y = XB + E\end{equation}$$

Where (we assume that we have $n$ predictor variables and $m$ data points / observations) $Y$ is an $m \times 1$ vector of values of the dependent variable, $B$ is an $(n+1)\times 1$ vector of the coefficients, $X$ is an $m\times (n + 1)$ matrix of the independent variables (including the constant term / y-intercept) and $E$ is an $m\times 1$ matrix of the error values:
$$
\begin{equation}

Y = 
\begin{pmatrix}
y_1 \cr y_2 \cr ...\cr y_m \cr
\end{pmatrix}

, B = 
\begin{pmatrix}
\beta_0 \cr \beta_1 \cr ...\cr \beta_n \cr
\end{pmatrix}

, X = 
\begin{pmatrix}
1 & x_{11} & x_{12} & ... & x_{1n} \cr
1 & x_{21} & x_{22} & ... & x_{2n} \cr
... & ... & ... & ... & ... \cr
1 & x_{m1} & x_{m2} & ... & x_{mn}
\end{pmatrix}

, E = 
\begin{pmatrix}
\epsilon_0 \cr \epsilon_1 \cr ...\cr \epsilon_m \cr
\end{pmatrix}

\end{equation}
$$

If we have either auto-correlation or heteroscedasticity, that means the variance of the error terms must be represented by some matrix. Therefore we would have that: $$\begin{equation}
Var(E) = \Omega
\end{equation}$$

Where $\Omega$ represents an $n \times n$ matrix of the variance of the error terms. Note that variance can be computed through the following equation:
$$\begin{equation}
Var(E) = \sqrt{\frac{\Sigma_{i=1}^n(x_i-\bar{x})^2}{n}}
\end{equation}$$

Now we wish to transform the original regression equation that is found in equation 1 such that the error terms have constant variance and no correlation. We will use a matrix $\omega$ to do this, $\omega$ must meet the following requirement:
$$\begin{equation}
\omega\Omega\omega^T = I
\end{equation}$$

$\omega$ can be computed as the matrix square root inverse of $\Omega$, this process is somewhat involved and will be discussed below:

* First an eigenvalue decomposition must be performed on $\Omega$, such that we have $\Omega=Q \Lambda Q^T$ where $Q$ is an orthogonal matrix whose columns are the eigenvectors of $\Omega$ and $\Lambda$ is a diagonal matrix whose diagonal elements are the eigenvalues of $\Omega$.

* Now we must take the inverse square root of $\Lambda$, since $\Lambda$ is a diagonal matrix, this can be as follows: $\Lambda^{-1/2} = diag(\lambda_1^{-1/2}, \lambda_2^{-1/2}, ..., \lambda_n^{-1/2})$

* Finally we rebuild $\Omega$ to obtain $\Omega^{-1/2}$ as such: $\Omega^{-1/2} = Q\Lambda^{-1/2}Q^T$

Now that we have $\Omega^{-1/2}$ and we know that $\omega = \Omega^{-1/2}$, we can now use $\omega$ to transform our regression equation:
$$\begin{equation}
\omega Y = \omega X B + \omega E 
\end{equation}$$

We will define some new variables for simplicity: $y^*=\omega Y, x^* = \omega X, \epsilon^* = \omega E$, allowing us to obtain:
$$\begin{equation}
y^* = x^* B + \epsilon^* 
\end{equation}$$

In the transformed model stated in equation 7, the variance of the error terms would be constant and there would be no correlation ($Var(\epsilon^*)=I$).

Now [OLS regression](Ordinary%20Least%20Squares%20Regression%20(OLS).md) can be used on equation 7 to obtain the estimates of the coefficients:
$$\begin{equation}
B = (x^{*T}x^*)^{-1}x^{*T}y^*
\end{equation}$$

Substituting in $y^*=\omega Y, x^* = \omega X, \epsilon^* = \omega E$:
$$\begin{equation}
B = (X^T\omega^{T}\omega X)^{-1}X^T\omega^{T}\omega Y
\end{equation}$$

Substitute in that $\omega^T\omega = \Omega^{-1}$:

$$\begin{equation}
B = (X^T\Omega^{-1}X)^{-1}X^T\Omega^{-1}Y
\end{equation}$$