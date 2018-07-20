Chapter 2 Describing Population
================================

## 2.1 Populations and Variables

#### 2.1.1 Qualitative Variables

#### 2.1.2 Quantitative Variables

#### 2.1.3 Multivariate Data 

variables that contain more than one variable


## 2.2 Population Distributions and Parameters

#### 2.2.1 Distributions

probability density function

mode: value under the peak of probability density function

multimodal distribution: a distribution with more than one model.


#### 2.2.2 Describing a population with Parameters

#### 2.2.3 Proportions and Percentiles

proportion = (numer of units in population having characteristic A) / N

#### 2.2.4 Parameters Measuring Centrality

mean median mode
```r
  mean: mean(vector)
  
  median: median(vector)
  
  mode: 
    mode <- function(v) {
      uniqv <- unique(v)
      uniqv[which.max(tabulate(match(v, uniqv)))]
    }
```

#### 2.2.5 Measure of Dispersion

standard deviation.   variance
IQR (inter-quantile range ) 75th percentile - 25th percentile

```r
  std.dev = sd(vector)
  
  variance = var(vector)
  
  IQR = iqr(vector)
```

#### The Coefficient of Variation

cv = (sd/mean)*100%

cv indicates the variability in the population compared with the mean of the population. 

When it's large, it means the population varies greatly relative to the mean of population.

#### Parameters for Bivariate Populations

bivariate distribution: Pab = proportion of pairs in population where X=a and Y=b, where Population is (Xi,Yi)

Corr(X,Y) correlation coefficient , [-1,1]
![](http://www.r-tutor.com/sites/default/files/images/numerical-measures10x.png)


## 2.3 Probability

#### 2.3.1 basic rules page 48

#### 2.3.2 Conditional Prob page 50

#### 2.3.3 Independence page 52

p(ab) = p(a) * p(b)

## 2.4 Probability Models

#### 2.4.1 Binomial Probability Distribution

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/8d166dfa3dfbfbf2e2672144bf2d9f25a1c77503)

#### 2.4.2 Normal Probability Model

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/a4145febbfa700e8711b7bc87fa1dbf9ec37f906)

for R, learn how to generate random sequence and how to calculate the critical factor

```r
# for Z critical factor
qnorm(p, mean = 0, sd = 1, lower.tail = TRUE, log.p = FALSE)

# for random sequence
rnorm(n, mean = 0, sd = 1)
```

#### 2.4.3 Z scores




