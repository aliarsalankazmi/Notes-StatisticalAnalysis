Notes pertaining to univariate/multivariate statistical analysis
================================================================


## Data Types

1. Non-Metric
  - Ordinal: Categorical variables that denote some kind of order.
  - Nominal: Categorical variables that only denote nomination and not any order.
2. Metric
  - Ratio: Such variables allow one to measure intervals between their values, as well as ratios - they have an absolute zero point.
  - Interval: Such variables allow one to take intervals between values, only.
3. Summated Scales: In such a scale, several variables are joined in a composite measure.


## Basic Statistics

* Statistical Population: A *complete* set of items that share at least a single property.
* Sample: A *set* of data collected from the Statistical Population.
* Frequency Distribution: A set of data that denotes how often (that is, the *distribution*) each value occurs in a sample. These distributions may take up different forms: Normal distribution, T-distribution, Binomial distribution, etc.
* Central Tendency: Where the centre of a frequency distribution lies. There are several ways of finding the central tendency:
  - Mean
  - Median
  - Mode
* Dispersion of distribution: The spread of values in a variable. Simplest way to check this is to subtract the largest value from the smallest, or to check the *range*.
  - Since range gets affected from the presence of extreme scores, often the top and bottom 25% of values are removed and only the range of the middle 50% is calculated - the *interquartile range*. Although interquartile range is not affected by extreme values, it has the disadvantage of removing a lot of data.
ok
  
                data(faithful)
                freqDist <- table(faithful$eruptions)
                hist(freqDist)
                myMean <- mean(faithful$eruptions)
                myMedian <- median(faithful$eruptions)
                myMode <- faithful$eruptions[order(faithful$eruptions, decreasing = TRUE)][1]
                deviationScore <- faithful$eruptions - mean(faithful$eruptions)
                #Sum of squared deviations OR Sum of squared errors OR Sum of squares
                SSD <- sum((faithful$eruptions - mean(faithful$eruptions))^2)
                myVariance <- SSD / length(faithful$eruptions) - 1
                myStdDev <- sqrt(myVariance)

* Using Frequency distribution to go beyond data
  - Probability distributions can be used to calculate the probability of getting particular scores, based on the frequency with which a particular score occurs in the distribution.
  - A problem might be that we do not have data with 0 mean and 1 standard deviation. However, any data can be converted to have 0 mean and 1 standard deviation - using the centering and scaling techniques.
  - Subtract a value from the mean to center it, and divide it by the standard deviation to scale it. These are known as Z-scores
  - Certain Z-scores are more important, as their values cut off certain percentage distributions. For example, Z-score = 1.96 cuts off the top 2.5% of the distribution, and Z-score = -1.96 cuts off the bottom 2.5% of the distribution. Combined, this Z-score cuts off 5% of the distribution; 95% of the Z-scores lie between -1.96 to +1.96. Other important scores are 2.58 and 3.29, which cut off 1% and 0.1% of the distribution.
  - Through this technique, we can see whether data is likely or unlikely to occur in a particular distribution.

## Simple Statistical Modelling and Assessment

* One simple statistical model is the mean - it is a hypothetical value that may not necessarily be observed in the data.
* For any statistical model, there are ways to assess the fit:
  - We may calculate how much our predicted data (the mean) differs from the actual data - **deviance**. Overall deviance may be found by summing up all deviances. Since a simple sum of the deviances would produce 0 (*due to the fact that some deviances would be the result of overestimation while others that of underestimation*), we shall square the deviances and then add up. This is called the **sum of squared errors**.
* However, the **sum of squared errors** is dependent on amount of data available - the more data points, the higher the Sum of squared errors' value. To overcome this problem, the Sum of squared errors is divided by the number of data points, to calculate the **average error**. If, however, we intend to find *not* the average error, but the error present in the population as a whole, we divide the Sum of squared errors with (number of data points - 1) - this is called **variance**.
* In addition to the variance, the *standard deviation* may be found, which is the application of a square root to the variance. 
* In such a manner, the sum of squared deviations, variance, and standard deviations can all be used to measure the goodness of fit of a model, in addition to being used for measuring the dispersion of data.

* Another way of modelling is *not* to check if our model is a good fit to the sample, but if it is a good fit to the **population** from which the sample was obtained.
* 
