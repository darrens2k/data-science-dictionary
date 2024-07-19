# Ordinary Least Squares Regression (OLS)

Credits: XLSTAT, The Coding Train, Isik Bicer, Standford University

### What is it?

OLS regression is a method that can be used to determine the values of the coefficients in linear regression.

### What do we use it for?

Often times it is applied to determine or estimate the coefficients of a linear regression.

### How does it work?

There will be separate explanations written up for the cases of simple and multiple linear regression. Please see the entry about Linear Regression for more information about simple and multiple linear regression.

OLS aims to minimize the squared distance of each data-point to the regression line, which translates to minimizing the squared error. The reason that the squared distance/error is used is to remove the potential of negative and positive errors cancelling each other out. That could result in an overall 0 error, for a line that is very poorly fit.

#### OLS for Simple Linear Regression

As a reminder, the equation we are attempting to solve with simple linear regression is of the form: $$\begin{equation}y = ax + b\end{equation}$$

Through this method, $a$ can be computed through the following equation: $$\begin{equation}a = \frac{\Sigma_{i=0}^n(x_i-\bar{x})(y_i-\bar{y})}{\Sigma_{i=0}^n(x_i-\bar{x})^2}\end{equation}$$

Where $\bar{y}$ and $\bar{x}$ refer the means of the dependent and independent data respectively. The following equation can be used to obtain $b$, it is obtained by re-arranging the regression equation: $$\begin{equation}b = \bar{y} - m\bar{x}\end{equation}$$

#### OLS for Multiple Linear Regression

You may recall that the regression equation for multiple linear regression takes the following form: $$\begin{equation}\hat{y} = a_1x_1 + a_2x_2 + ... + a_kx_k + b\end{equation}$$

For this explanations we will convert this into vector equation that will be more compact, it will allow for the mathematics to be greatly simplified as well. We will assume that we have $n$ predictor variables and $m$ data points / observations. In this method we will create $m$ instances of equation 4, one for each data point. We will utilize an equation of the form: $$\begin{equation} Y = XB + E \end{equation}$$

Where $Y$ is an $m \times 1$ vector of values of the dependent variable, $B$ is an $(n+1)\times 1$ vector of the coefficients, $X$ is an $m\times (n + 1)$ matrix of the independent variables (including the constant term / y-intercept) and $E$ is an $m\times 1$ matrix of the error values:
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

Now we can use the definitions laid out to compute the squared error as $E^TE$:
$$
\begin{equation}

E^TE = (Y - XB)^T(Y-XB)

\end{equation}
$$

After simplifying this becomes:
$$
\begin{equation}

E^TE = Y^TY-2B^TX^TY+B^TX^TXB

\end{equation}
$$

Now we need to minimize the quantity solved in equation 8, we will first take its derivative and then set its derivative equal to 0.
$$
\begin{equation}

\frac{\partial E^TE}{\partial B} = -2X^TY+2X^TXB=0

\end{equation}
$$

Now we must isolate for B in equation 9, this is a non-trivial task and I will not walk through all of the steps here. If one does desire to see the full derivation of this, you an simply google "OLS Matrix Method". We finally obtain: 
$$
\begin{equation}

B=(X^TX)^{-1}X^TY

\end{equation}
$$

Equation 10 can then be used to estimate the coefficients off of the data, the coefficients can be used in $\hat{y}=XB$ to compute predicted values of y, and then the error values can be computed as $\epsilon=y-\hat{y}$. Then all of the values in equation 5 can be filled in, and the equation can be used for predictions.

#### Assumptions of OLS
The assumptions made by OLS are the same as those made by Linear Regression, see the Linear Regression entry for more info.