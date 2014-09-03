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
  - While the above acknowledge only some part of data, the **variance** and **standard deviation** may be used alternatively, for checking the dispersion of data.
  
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

* Another way of modelling is *not only* to check if our model is a good fit to the sample, but if it is a good fit to the **population** from which the sample was obtained.
* The above approach takes account of the fact that whenever any calculation is performed on a sample of data, this sample is usually only a subset of the entire population. Other 'subset's of the population may slightly differ in their values - this is known as **sampling variation**. If means are calculated for all sample data generated from a population, the standard deviation between these sample means would provide us with a measure of variability between these means of different samples. This is known as the **Standard error of the mean**.
  - We also cannot collect hunderds of samples and then calculate the standard error of the mean. To our benefit, it was demonstrated by statisticians that as samples get large, their sampling distribution has a normal distribution, with a mean equal to the population mean. This is known as the **Central Limit Theorem**, and is useful in that given a large sample size, the standard error can be approximated by calculating the standard deviation of the sampling distribution.
    - **Three principles of CLT**:
      1. The mean of the sampling distribution is the same as the mean of the population.
      2. The SD of the sampling distribution is the SQRT of the variance of the sampling distribution.
      3. The shape of the sampling distribution is approximately normal if either a) N>=30 or b) the shape of the population distribution is normal.
  - In case the sample size is small, the distribution is known as **t-distribution**.
* Yet another approach to assess the accuracy of a sample mean as an estimate of the population mean is to calculate boundaries within which the population mean will be - these are called **confidence intervals**.
  - Typically, 95% (and sometimes 99%) confidence intervals are used. A 95% confidence interval implies that for 95% of the samples collected, the population mean will fall within this boundary.
  - These intervals can be calculated in the following manner: 
    - As mentioned previously, the z-scores of 1.96 and others are important because these say that, for example, 95% of the z-scores fall within -1.96 and +1.96. With large samples, as per the Central Limit Theorem, the sampling distribution will be normally distributed.
    - Given a normal distribution, lower boundary for CI: mean - (1.96 x SD)
    - Given a normal distribution, upper boundary for CI: mean + (1.96 x SD)
    - Given a t-distribution, lower boundary for CI: mean - (t_n-1 x SD)
    - Given a t-distribution, upper boundary for CI: mean - (t_n-1 x SD)

* *Yet* another way of assessing how well a mode fits our data is by using the **test statistic**.
  - Test statistic = variance explained by model / variance not explained by model
  - Once the test statistic is calculated, the probability of getting this value is then looked up.

* Statistical Significance VS. Statistical Power
  - All statistical techniques (except cluster analysis and perceptual mapping) are based on statistical inference of a population's values or relationships among variables from a randomy drawn sample of the population. Interpreting statistical inferences requires the researcher to specify the acceptable levels of statistical error that result from using a sample.
  - Type I error: the probability of rejecting the null hypothesis when it is actually true (false positive).
  - Type II error: the probability of NOT rejecting the null hypothesis when it is actually false.
  - Statistical power influenced by: effect size, alpha level (type I error), sample size.

* Weaknesses and their remedies for Null Hypothesis Significance Testing (NHST)
  - Weakness: Biased by sample size
    - In regression:
      - p-value is based on t-value
      - t=B/SE (B is regression coefficient, SE is Standard Error)
      - SE=SQRT(SS.Residual/(N-2))
  - Remedy: Supplement all NHSTs with estimates of effect size
    - In regression:
      - report standardised regression coefficients and the model R-squared.
  - Weakness: Arbitrary decision rule (the cutoff value [alpha] is arbitrary)
  - Remedy: supplement all NHSTs with estimates of effect size
  - Weakness: Yokel Lokel Test - NHST ecnourages weak hypothesis testing
  - Remedy: learn other forms of hypothesis testing,consider multiple alternative hypotheses
  - Weakness: Error prone
  - Remedy: replicate significant effects to avoid long-term impact of Type-I errors, obtain large and representative samples to avoid Type-II errors.
  - Weakness: Logic becomes probabilistic in NHST
    - Modus Tollens in NHST becomes probabilistic
    - (IF p then q; NOT q; THEREFORE NOT p)
    - (IF null-hypothesis correct, then these data are HIGHLY UNLIKELY; Data have OCCURREDl; THEREFORE, the null hypothesis is HIGHLY UNLIKELY)
  - Remedy: Don't use NHST | remember p=P(D|H-null) | report confidence intervals only | Apply bayesian learning

* Measures of effect size
  - Many measures: Cohen's d, Pearson's correlation coefficient, odd's ratio, etc.
  - Effect sizes provide a measure of the importance of an effect. These are calculated for samples, and the same could be used to estimate the effect size of the entire population.
  - Effect sizes depend on 3 other statistical properties:
    - sample size,
    - the probability level at which we will accept an effect as being statistically significant (a-level)
    - statistical power (the ability of a test to detect an effect of size

## Checking Statistical assumptions in data

* To check if a distribution follows **normality**:
  - Plot histograms (especially for large data sets)
  - Plot QQ-Plots (when line sags below or rises above diagonal, it indicates kurtosis is different from normal distribution, while if the line has an S-shaped curve, it indicates positively or negatively skewed data)
  - Use Shapiro-Wilk test (with large sample sizes, small deviations from normality can produce significant results)
  - Use Komogorove-Smirnov test for Kurtosis 
* To check for **homogeneity/heterogeneity** of data:
  - Levene test (with large sample sizes, small deviations from normality can produce significant results)
  - Hartley's F-max (or the Variance Ratio)
  - Box's M-test (tests for homogeneity of variance OR the equality of covariance)
* To check for **linearity**:
  - Examine residuals, as any non-linear portions of relationships will be shown
  - Correlated errors *must* be treated!

## Transforming Data

* Data transformations are usually carried out for 2 reasons:
  - To correct violations of statistical assumptions
  - To improve relations between variables
  - When a transformation is applied, it is said that the same must be applied to all data - not in the manner that to one variable, a log transformation is applied, whereas to others an Inverse.
* To deal with outliers:
  - Remove outliers
  - Transform data
  - Change data manually
    - Highest score plus 1
    - If outlier is a z-score, convert it back to original value
    - Mean + 2 Standard Deviations
* To achieve normality:
  - If distribution is flat (negative kurtosis), use **Inverse**.
  - If distribution is negatively skewed, use a **Square** or a **Cube**.
  - If distribution is positively skewed, use a **Logarithm** or a **Square root**.
* To achieve homoscedasticity:
  - If the cone opens to the right, take **Inverse**.
  - If the cone opens to the left, take a **Square root**.
* To achieve linearity:
  - Can use squares, cubes, square-roots, logs, inverse, etc.
* However, transformations to data make its interpretation difficult, as the values are changed from original ones.
* Also, transforming data means that the hypothesis being tested is changed (when using a log transformation and comparing the means, we change from comparing arithmetic means to comparing geometric means).

* If no transformations work/are impossible to implement, then either of the following 2 methods may be invoked:
  - Use trimmed values (e.g. trimmed mean)
  - Bootstrapping (samples tend towards normality as they get larger - a very clever technique)

## Measures of Association

* Different ways to measure association between variables.
* Some ways allow identification of directions for relationships (for example, correlation). Others do not show this direction (chi-squared statistic, Cramer's V, etc.).

### Correlation Analysis

* The simplest way to check if two variables are associated is to check if they *covary*.
* A cross-product of two variables' deviations, added for all variables and averaged (divided by total values - 1) is known as **covariance**.
* However, a problem faced when calculating covariance is that it is affected by scales of measurement. Covariance, thus, cannot be an objective measure of association for two variables.
* To obtain a standardised covariance (also known as correlation coefficient), the covariance is divided by the multiplied result of standard deviations for two variables - this gives us the covariance in standard deviation units.
* This is also known as Pearson product-moment correlation coefficient.
* We may perform a **Null Hypothesis test** for the correlation coefficient (thinking whether the observed correlation coefficient is likely or unlikely to occur if there is no effect in the population) in two ways:
  - Converting the correlation coefficient to a Z-score and then this by the standard error (Z-score is computed because we know the probability of a given Z-score, as long as the distribution is normal. Since it isn't normal for a correlation coefficient, it is divided by the standard error)
  - Using a t-statistic, the formula for which is: (correlation coefficient*sqrt(N - 2)/sqrt(1 - correlation coefficient ^2))
* Alternatively, we may compute the confidence intervals for a correlation coefficient (after converting the correlation coefficients to Z-scores and computing the standard error. The standard error of the mean is just dividing the Standard Deviation by the sqrt(N) where N = total number of values).
* Another possible method is to use **bootstrapping** to repetitively draw samples from a sampling distribution, and compute correlation over each of the drawn samples. This is very easy to do with R.
  - Once the values for the CI are calculated, we need to convert them back to Correlation coefficients.
* There are **two** types of Correlations:
  - Bivariate:
    - Pearson's Correlation Coefficient
    - Spearman's Rho
    - Kendall's Tau
  - Partial

* Pearson's Correlation Coefficient
  - Assumptions:
    - Variables are of interval type (continuous vs. continuous)
    - For checking statistical significance, data are distributed normally.
    - Linearity and constant variance
  - This correlation is for linear relationships.
  - Squaring the correlation coefficient (known as the Correlation of Determination, R^2) is a measure of the amount of variability in one variable shared by the other.
* Spearman's Rho
  - Assumptions:
    - Variables are ordinal, ratio, or interval (ordinal vs. ordinal)
    - Variables are ranked
  - This correlation is for monotonic relationships
  - When data is not normal, the Spearman's Rho can be used, as it is non-parametric.
* Kendall's Tau
  - This is useful if Spearman's Rho is to be calculated, but the data set is small with a lot of variables at the same rank.
* For Continuous vs. Ordinal variables: Biserial correlation *(use `polyserial()` from `ploycor` package)*
* For Continuous vs. Nominal variables: Point-Biserial correlation *(use simple correlation in R)*

* For Ordinal vs. Nominal variables: use Rank Biserial
* For Nominal vs. Nominal variables: use Phi Coefficient, Chi-Squared Statistic, Contingency Coefficient, or Cramer's V
  - These do not show the direction of relationships
  - Phi used for variables when each has exactly 2 possible outcomes; adjusts sample size. Phi = sqrt(chi-squared/n)
  - Contingency Coefficient used when each variable has 3 or more possible outcomes. C = sqrt(phi^2/1+phi^2)
  - Cramer's V used when variables have unequal number of possible outcomes. V = (phi^2/t) OR V = sqrt(chi-squared^2/nt) where t = min(nrow-1,ncol-1)

* For partial correlations:
  - use the `ggm` package's `pcor()` function

* For **comparing correlation coefficients**:
  - Independent correlation coefficients, convert to Z-scores (to make the distribution normal and calculate the standard error), and calculate the difference of these Z-scores
  - For dependent correlation coefficients, use the t-statistic

* For calculating the **effect size**:
  - Correlation coefficients for Pearson's and Spearman's are the effect sizes. However, the effect size of Kendall's Tau and Pearon's and Spearman's are not comparable, as Kendall's Tau is always smaller than Spearman's (and Pearson's).

* It is worth bearing in mind that **outliers** do impact correlation coefficients. Especially in small samples, outliers can greatly affect correlation strengths.
* Correlation coefficients can be converted to **distance/dissimilarity** measure in the following manner:
  - dissimilarity measure = (1 - correlationCoefficient)/2
* A dissimilarity measure can be converted to a **similarity measure** by: 1 - dissimilarityMeasure

### Association between categorical data

* Categorical data is usually measured by frequencies.
* Frequency data for categorical variables can be cross-tabulated to produce a **contingency table**.
* On such a table, the **chi-squared test** can be performed - this statistic compares the frequencies observed with those that can be expected.
  - The standard equation used to evaluate a model is: Deviation = sum of (observed - model)^2, where model is the expected frequencies that we calculate from the contingency table.
  - This equation can also be used for categorical data, with slight modification of dividing by model scores. This produces standardised deviations.
  - To calculate the *model* (or the *Expected frequencies*): (RowTotal * ColumnTotal)/  Total
  - Chi-squared statistic = sum((ObservedValues - ExpectedFrequencies)^2 / ExpectedFrequencies)
  - Once this is calculated, we find the degrees of freedom = (NumberOfRows - 1)(NumberOfColumns - 1)
  - Chi-squared test assumes independence of data (each item/entity contributes to only one cell of the contingency table), and that expected frequency values in contingency tables must be > 5.
  - One problem is that the sampling distribution of the chi-squared test statistic has an *approximate* chi-squared distribution. Due to this, the expected cell frequencies in each cell must be > 5.
  - In case we have small samples, **Fisher's Exact Test** could be used to compute exact probability of the chi-squared test statistic.

* Another method to measure association is **likelihood ratio statistic**.
  - The rationale behind this method is to first create a model for which the probability of obtaining the observed set of data is maximised. Then, this model is compared to the probability of obtaining the observed data under the Null hypothesis.
  - The formula for likelihood ratio is: 2 x sum(observedValue x ln(observedValue/expectedValue))
  - This statistic also has a chi-squared distribution.
  - This statistic is also useful in small samples, but can be used with large samples too.
* To calculate the **effect size** for categorical variables, the **odds ratio** is used.
  - Odds ratio for a given b = prob(a|b)/prob(a|not b)

* These measures do **not** show the *direction* of relationship between variables.

* When a large number of variables are involded, the **log-linear** analysis for categorical data can be performed.
