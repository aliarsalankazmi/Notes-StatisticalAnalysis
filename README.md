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
  
        data(faithful)
        freqDist <- table(faithful$eruptions)
        hist(freqDist)
        myMean <- mean(faithful$eruptions)
        myMedian <- median(faithful$eruptions)
        myMode <- faithful$eruptions[order(faithful$eruptions, decreasing = TRUE)][1]
        deviationScore <- faithful$eruptions - mean(faithful$eruptions)
        Sum of squared deviations OR Sum of squared errors OR Sum of squares
        SSD <- sum((faithful$eruptions - mean(faithful$eruptions))^2)
