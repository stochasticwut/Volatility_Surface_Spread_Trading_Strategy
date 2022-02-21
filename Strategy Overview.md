# Strategy Overview

This strategy makes important use of volatility cones to define a trading strategy over equities. The idea of determining if options are expensive or cheap using volatility cones comes from Burghardt and Lane (1990). The general idea is that the strategy finds opportunities by identifying instances where the current implied volatility of (ATM) options are outside the volatility cone. A clear example of a succesful volatility cone strategy would be when the IV of an ATM call option that is 30 days from expiry is higher than the 30-day volaility cone. This suggests that the IV of the option should fall as it goes back within historical boundaries. Shorting the call option would therefore lead to a positive return.

## Constructing Volatility Cones

Constructing the volatilty cones makes use of price data of the underlying asset. 

From the price series, generate a 1-day return series. Compute an M-day volatility series by taking the rolling M-day standard deviation and annualizing it (x sqrt(252)). For each M-day volatility series we can apply a J-day rolling window where we assign a quantile to each data point. This means that over for example 100 days we might have 10 90th percentile volatilities. We can take the average (with or without weighting like exponential) and this generates the 90% percentile volatility cone for M days to expiry options. We can do this for many different percentiles and we have different boundaries that we can use for our trading strategy.

We should use the adjustment factor by Hodges and Tompkins (2002) (see p. 40 of the Sinclair textbook)

## Choices:

Which volatility cone to use? 90th, 80th... percentile? Does it have to be symmetric? 

If trading volatility of individual equities/futures, we can use a benchmark to determine the spread. For example, if we are monitoring the IV of AAPL vs the volatility cone, we should put it in perspective of the spread that exists between the Nasday IV and its volatility cone.

Which options? Long term expiry likely less efficient (Burghardt and Lane (1990))

How much data? - "but two years or more of data would seem to be adequate, at least if here has been no fundamental change in the forces driving the market" Burghardt and Lane (1990)

We can use volatility cones in the context of another prediction algorithm. For example, in Sinclair they mention GARCH time series model for volatility prediction. We can trade if both the GARCH prediction and IV are outside the volatility cone. 






