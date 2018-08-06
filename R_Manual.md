## 1. Set Work Directory
```r
setwd("your work directory")
```

## 2. Load csv to the environment (it's enough)

```r
# csv
df <- read.csv( "fecfat.csv", header = TRUE )
```

## 3. plots

#### 3.1 scatter plot
```r
plot(df$response ~ df$explanatory)
```

#### 3.2 individual plot & baxplot

```r
# The linear-regression model will try to predict glucose from physact and assumes
# any resulting error is additive iid normal with zero mean and constant variance.
# We are looking at the variation within each physact level to see if the error assumption
# looks valid.  We should be suspicious of large outliers, skewness, gaps, or large
# inequalities in the ranges.  Here, there look to be a fair number of high-glucose
# outliers but these are very close to the whisker limit at 1.5 times the inter-quartile 
# range.  There is one strong low-glucose outlier in the "somewhat more active" set.
# Both might merit some further investigation.

# individual plots for each level of physact
stripchart(df3$glucose ~ df3$physact, vertical=TRUE)
# baxplot for each level
boxplot(df3$glucose ~ df3$physact)
```

#### 3.3 histgram and normal probability plots of residuals
```r
# Both the histogram and the normal-probability plot are a direct check on how much
# the error residuals look like they are normally distributed.  Here we see some
# slight deviations from normality since the histogram looks a little asymetric
# and the normal-probability plot is not quite linear, especially near the ends.
# The deviations look consistent with the outliers seen in Part d.

resid1 <- linear.mod3$residuals
# histgram
hist(resid1)
# normal probability plots
qqnorm(resid1)
qqline(resid1)
```
