java c
Time Series Analysis
Coursework
Handout: Tuesday 25th February 2025.
Deadline: Submit electronic copy to the turnitin assignment dropbox on Blackboard before 1pm Wednesday 19th March 2025.
This coursework is worth 10% of your mark for Time Series Analysis.
There are 2 questions. Together they are worth 40 marks
You must write up a report (MS Word, LATEX or a notebook (e.g. Jupyter) is fine), including necessary mathematical derivations and all your code within the main text (not as appendices and no screen shots). You must submit a pdf that can be fully read by Turnitin.
Plots and tables should be clear, well labelled and captioned. Comment your code. Up to 5 marks may be deducted from your score for a poorly presented report.
For the computational elements, you must use R or Python. It is up to you which you choose. Both are equally valid.
You may use any results from the notes you wish, but you must properly cite them.
Your report must be no more than 12 pages (not including a cover page). This does not mean you have to use all 12 pages - you should be able to do this in fewer than 12 pages.
Put your CID number clearly at the top of your report.
NB: Stationarity by itself always means ‘second-order’ stationarity. {∈t} denotes white noise with mean zero and variance σ2∈. Assume {∈t} is Gaussian/normal here. You can assume a sampling interval of ∆t = 1 throughout.
Question 1
(a) Simulating time series is an essential component of research, allowing theory to be verified and methodology to be tested and benchmarked. In this question you will write your own code to simulate a sequence X1, . . . , XN from a stationary Gaussian/normal AR(2) process.
The tricky thing here is that in order to simulate X1 you need to know X0 and X−1. A stochastic process goes from times −∞ to ∞ so that these three variables must be generated to satisfy the stationarity conditions. Let’s see how we can do this. Consider the covariance matrix for [X0, X−1]T. It takes the form.

We can carry out a Cholesky decomposition of D by finding C such that D = CCT where C is a lower triangular matrix.
Now consider a vector Y = [Y1, Y2]T where Y1 and Y2 are each standard Gaussian/normal and independent. Then the covariance of the vector CY is CICT = CCT = D, the required covariance structure.
Using the above scheme, write your own function AR2(xi,sigma2,N) to simulate N values X = [X1, . . . , XN ] from a zero mean Gaussian AR(2) process parameterised as

The input parameters are ξ := (ξ1, ξ2), σ2∈ and N. You may use an inbuilt function to compute the Cholesky decomposition.
HINT: You will need the following form. of the autocovariance sequence for a AR(2) process parametrised in this way (p. 94, Brockwell  Davis, Time Series: Theory and methods, Springer-Verlag, 1987)

Your answer to this question is your code.
[4 marks]
(b) Choose N = 6 and ξ1 = 10/9, ξ2 = 2, σ∈2 = 1. Generate M = 100 independent sample vectors X1, . . . , XM using your code from Part (a) and form. an estimate of the symmetric Toeplitz covari-ance matrix of the vector [X1, . . . , X6]T via

Let ˆs0, . . . , sˆ5, be the estimated variance and covariances in the first row of Σˆ. The true values are s0, . . . , s5. Calculate the error a = Σ5j=0(ˆsj − sj )2.
Repeatedly simulate these steps (independently) 500 times to get 500 values of a and find the average error, ¯a for M = 100.
Do the above also for M = 150 to 500 in steps of 50, so that altogether you have values of ¯a for M = 100 : 50 : 500 and save these.
For M = 500 only, compute the average value of Σ over the 500 repeat simulations, and ˆ print it out together with the true Toeplitz covariance matrix
[4 marks]
(c) Let N = 100. Generate X = [X1, . . . , XN ]T and estimate the variance and autocovariances s0, . . . , s5 via

Calculate the error b = Σ5j=0(ˆsj − sj )2.
Repeatedly simulate these steps (independently) 500 times to get 500 values of b and find the average error, ¯b for N = 100.
Do the above also for N = 150 to 500 in steps of 50, so that you have values of ¯b for N = 100 : 50 : 500.
Plot the values of ¯b against the corresponding number of samples, N, using a dashed line.
On the same figure, plot the saved values of ¯a against the corresponding number of samples, M, using a solid line.
[4 marks]
(d) Given your plots of ¯a and ¯b versus sample size, suggest a reason for the marked difference in estimation error between the two methods for the same sample size. Hint: You might find it informative to rerun Parts (b) and (c) using a white noise process instead of an AR(2).
[4 marks]
Question 2
You each have your own individual time series x1, ..., x60 which can be retrieved by downloading your time series from this directory. The number of your time series can be found in the accompanying file time series number.pdf.
This is 5 years of monthly sales data for a company, from January 2020 to December 2024. For most of this question, you’ll assume it’s the 1st January 2024 and you’ve been tasked with forecasting annual sales for the next 12 months. Therefore you only have the first four代 写Time Series AnalysisPython
代做程序编程语言 years of data x1, ..., x48. You’ll use x49, ..., x60 in Part (h).
(a) From inspection, you’ll see the time series has an increasing trend. Write your own function that fits an ARIMA(p, d, 0) model using the least squares method. Recall, this means you will model {Xt(d)} as an AR(p) process.
[3 marks]
(b) It can be shown that for a stationary Gaussian AR(p) process, the AIC reduces down to
AIC = 2p + N ln(ˆσ2∈).
For p = 1, 2, ..., 5 and d = 2, 3, 4, fit an ARIMA(p, d, 0) model. Under the assumption of Gaussian-ity, create a 3 × 5 table to neatly display the AIC for each value of p and d.
[2 marks]
(c) Which order model do you select as being the best fit for your data? Report d, p and the p + 1 estimated parameter values.
[1 mark]
(d) This model may be the best fit out of those you’ve considered, but it does not mean it’s a good fit. A common approach to determine this is to do a residual analysis.
Consider an AR(p) model of the form. Yt − φ1,pYt−1 − ... − φp,pYt−p = ∈t, where {∈t} is a white noise process. Given a time series y1, ..., yN , for a chosen order p and associated set of estimated parameters {φˆ1,p, ..., φˆp,p}, the residuals are {ep+1, ..., eN }, where
et = yt − φˆ1,pyt−1 − ... − φˆp,pyt−p.
Should the AR(p) process be a good fit, we would expected {ep+1, ..., eN } to be a an uncorrelated sequence. Conversely, if it is not, we would expect {ep+1, ..., eN } to contain autocorrelation. The Ljung-Box test is used to test for autocorrelation in residuals. It proceeds as follows:
• Compute all the residuals.
• The null and alternative hypotheses are
H0 : ep+1, ..., eN is a sequence of uncorrelated random variables
HA : H0 is not true.
The test statistic is

where n is the number of residuals, h is the number of lags being considered, and ˆρk is the estimate of the autocorrelation at lag-k for the residual sequence. Take ˆρk = ˆsk(p)/sˆ(0p). Hypothesis H0 is rejected if L > χ21−α,h, where χ21−α,h is the (1 − α)-quantile of the χ2h distribution.
You may use an inbuilt function for computing {ρˆk}, but otherwise, write your own code to apply the Ljunge-Box test for h = 24 (typical for monthly time series) at the α = 0.05 level. Make conclusions about your result.
[4 marks]
(e) In keeping with notation from the notes, at time t = N, we will let XN (l) represent the l-step ahead forecast of XN+l, and XN(d)(l) represent the l-step ahead forecast for XN(d+)l. Using the least squares model fitted in part (c), write your own function that computes X48(1), ..., X48(12). Note, you will initially be forecasting the values of X49(d), ..., X60(d). To get the forecasts for X49, ..., X60, you need to integrate out the values.
For example, if d = 2, then we know from the notes that Xt(2) = Xt − 2Xt−1 + Xt−2, and hence Xt = Xt(2) + 2Xt−1 − Xt−2. We therefore form. our forecasts recursively as

On a single axes, plot the true trajectory for t = 1, ..., 48 and the predicted trajectory for t = 49 to t = 60.
[4 marks]
(f) Point forecasts, like this, only have limited use. What is much more useful is supplying an accom-panying prediction interval. This is an interval which has some designated probability of containing the realised trajectory. The 95% prediction interval for YN+lis given as YN (l) ± 1.96σl, where σl is the standard deviation of the l-step forecast distribution.
So far in this question you have fit an AR(p) model to a dth differencing of x1, ..., x48. A naive estimator of σl, the standard deviation of the forecast errors for the dth differenced process is ˆσe√l. Here ˆσe is the sample standard deviation of the residuals. Use this to get the resulting standard deviation of the errors in forecasting X49, ..., X60 .
HINT: Consider writing XN(2)(l) = XN(2)+l+ηl, where ηlis the forecast error whose standard deviation is the σl estimated above. Then consider recursively propagating the errors through the integrating step shown in (e) to determine the standard deviation of the forecast error in XN (l). For this, you may assume that η1, ..., η12 are uncorrelated.
Add to your plot the upper and lower bounds of your 95% prediction interval for t = 49, ..., 60.
[3 marks]
(g) Use in-built functions in R or Python to fit an ARIMA or Seasonal-ARIMA (SARIMA) model to your time series. SARIMA models are not covered in the notes, but have a read about them. The recommended packages are forecast in R and statsmodels in python. You can use what-ever automated functionality you like to select the best model, assess the model fit, and forecast X49, ..., X60. Present an additional plot that shows your forecast and prediction intervals. HINT: E.g., if using forecast in R, the functions you might try include: ts(), auto.arima(), Arima(), checkresiduals(), forecast(), plot().
[5 marks]
(h) It’s now 1st Janunary 2025 and you have observed x49, ..., x60. Use the root mean squared errors in your forecasts, defined for a total of L steps ahead, as

to determine whether the model fit in part (g) performed better at forecasting than the ARIMA(p,d,0) model you used in part (e). [2 marks]



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
