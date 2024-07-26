# AutoRegressive Integrated Moving Average (ARIMA)

Credits: ChatGPT

### What is it?

This is a statistical method that is comprised of 3 parts:
* AutoRegressive (AR): The model determines the value of a variable based on its previous (lagged) values. In an AR(1) model, the current value of the variable is dependent on the immediately previous value of the variable.
* Integrated (I): This involves subtracting an observation from its previous observation, a process called differencing. This makes the time series stationary, meaning that its statistical properties (such as mean and variance) remain constant over time. This process removes trends from the data, ARIMA assumes that the data is stationary.
* Moving Average (MA): This part considers how the past errors affect the current value of the variable. Thus, this part aims to model the relationship between the time series and the errors of previous time steps. This is important as data can often contain "shocks", which are sudden changes, and using previous errors to influence current values helps account for these "shocks".

ARIMA models are usually denoted as ARIMA(p, d, q), where:
* p represents the number of lag observations to be considered in the AR part.
* d represents the number of times that observations are differenced in the I part.
* q represents the size of the moving average window in the MA part.

Note that ARIMA models are linear models, it is assumed that the relationship between the current value and its previous values and errors is linear. More will be written about this below in the assumptions section.

### What do we use it for?

ARIMA is most often used for time series analysis and forecasting.

### How does it work?

To explain how this model works, we will work through an example. We begin with an ARIMA(1, 1, 1) and the following time series data: 
$$
\begin{equation}
y = [5,6,7,10,11,13,14,18,20]
\end{equation}
$$

The data must first be differenced, and note that d = 1, so from each value we subtract the previous value. Notice that by doing this we reduce our data by d values (we lose the first data point). We will denote the differenced data by $y'$.
$$  
\begin{equation}
y' = [y_t-y_{t-1}]  
\end{equation}
$$

$$  
\begin{equation}
y' = [6−5,7−6,10−7,11−10,13−11,14−13,18−14,20−18]
\end{equation}
$$

$$  
\begin{equation}
y' =[1,1,3,1,2,1,4,2]
\end{equation}
$$

Now we must fit the AR(1) model, meaning that each value is dependent on the value that comes immediately before it. Thus we obtain:
$$  
\begin{equation}
y'_t = \phi y'_{t-1} + \epsilon_t
\end{equation}
$$

Where $\phi$ is the autoregressive parameter and $\epsilon_t$ is the error/noise term.

To estimate $\phi$ we can use [OLS](Ordinary%20Least%20Squares%20Regression%20(OLS).md) for simple regression (given that we have one variable). Thus we estimate $\phi$ as:
$$  
\begin{equation}
\phi = \frac{\sum_{t=2}^{8} y'_t y'_{t-1}}{\sum_{t=2}^{8} y_{t-1}'} = \frac{23}{33} \approx 0.697
\end{equation}
$$

Now to complete the MA(1) part, we must model $y'_t$ as a function of the previous error term, $\epsilon_{t-1}$:
$$  
\begin{equation}
y'_t = \epsilon_t + \theta\epsilon_{t-1}
\end{equation}
$$

Where $\theta$ can be estimated using the method of moments or maximum likelihood estimation, but for the sake of simplicity we will assume a value of 0.5.

The next step is to combine the AR(1) and MA(1) parts, to obtain the following equation:
$$  
\begin{equation}
y'_t = \phi y'_{t-1} + \epsilon_t + \theta\epsilon_{t-1}
\end{equation}
$$

Substituting in the above solved values:
$$  
\begin{equation}
y'_t = 0.697y'_{t-1} + \epsilon_t + 0.5\epsilon_{t-1}
\end{equation}
$$

The final step is to now use our model for forecasting, we can use equation 9 to forecast the future value. However, recall that differencing was done to obtain equation 9, to obtain the future value in the original scale of the data, we undo the differencing by using the following equation:
$$  
\begin{equation}
\hat{y}_{t+1} = y_t + \hat{y}'_{t-1}
\end{equation}
$$

Where $\hat{y}_{t+1}$ represents the un-differenced forecasted value, $y_t$ represents the un-differenced value of the time series at time t, and $\hat{y}'_{t-1}$ represents the differenced forecasted value.

#### Assumptions:
