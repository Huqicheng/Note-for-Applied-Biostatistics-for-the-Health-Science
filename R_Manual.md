## 1. Set Work Directory
```r
setwd("your work directory")
```

## 2. Load csv to the environment (it's enough)

```r
# csv
df <- read.csv( "fecfat.csv", header = TRUE )

# merge tables
merged.csv <- mutate(df, residual, fitted)
```

## 3. plots

#### 3.1 scatter plot
```r
plot(df$response ~ df$explanatory)
```

#### 3.2 individual plot & boxplot

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
# boxplot for each level
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
# density plot
plot(density(resid1))
# normal probability plots
qqnorm(resid1)
qqline(resid1)
```

#### 3.4 residuals versus index & residuals versus fitted value
```r
fitted1 <- fitted.values(linear.mod3)
plot(resid1 ~ fitted1)
plot( resid1 )

# These are mostly looking at the iid assumption for the error.  If there are suspicious
# patterns/variations in residuals versus index, the errors might be correlated (not independent). errors should be independent.
# If there are suspicious patterns/variations in residuals versus fitted values, the errors
# might not be identically distributed (equal-variance assumption not satisfied).  There don't
# seem to be any suspicious indications here. equal-variance assumption
```

#### 3.5 bar charts
```r
# vertical
barplot(counts, main="Car Distribution", xlab="Number of Gears")
# horizontal
barplot(counts, main="Car Distribution", horiz=TRUE,names.arg=c("3 Gears", "4 Gears", "5 Gears"))
# stacked bar plot
counts <- table(mtcars$vs, mtcars$gear)
barplot(counts, main="Car Distribution by Gears and VS",
  xlab="Number of Gears", col=c("darkblue","red"),
 	legend = rownames(counts))
 	
# side by side bar plot
# Or, Grouped Bar Plot
counts <- table(mtcars$vs, mtcars$gear)
barplot(counts, main="Car Distribution by Gears and VS",
  xlab="Number of Gears", col=c("darkblue","red"),
 	legend = rownames(counts), beside=TRUE)

```

#### 3.6 lines
```r
abline(intercept, slope)

# or using a sequence 
X = seq(0,30,by=0.1)
y = 2*X
plot(y~X)
```


## 4. Divided By Chapter

## 4.1 ANOVA
```r
# to fit a anova model
aov(formula=, data=)
# summary
summary(aov(formula=, data=))
# step() to see RSS and select useful explanatory variables
step(aov(formula=, data=))

# to fit a model with random effects using Error(explanatory var)
aov(y ~ fitted + Error(factor(var)))

# to check effects of the anova model
model.tables(aov.model) # type='effect' as a hint

```

## 4.2 Linear Regression
```r
# to fit a model
lm(formula=, data=)
# step() to see RSS and select useful explanatory variables
step(lm(formula=, data=))
# abline
abline(lm(formula=, data=))
# get residuals
linear.mod$residuals
# get fitted values
linear.mod$fitted.values
# confidence interval
confint(linear_model, 'typeNu', level=0.95)

# predict
predict.60 <- predict(fit, data.frame(AmbientTemp = 60)) 
```

## 4.3 Logistic Regression
```r
# to fit a model
glm(formula, data, family=binomial)
# step() to see deviance and select useful explanatory variables
step(lm(formula=, data=))
# pi
exp(coef[1] + coef[2]*x) / (1 + exp(coef[1] + coef[2]*x))
# odds
exp(coef[1] + coef[2]*x)
# log odds
coef[1] + coef[2]*x

# Logistic Regression with Most Likelihood estimator 
shuttle.logistic1 <- glm(Success~Temperature,family=binomial)
prob.mle <- exp(-15.043+.232*Temperature)/(1+exp(-15.043+.232*Temperature))

# Logistic Regression with least square estimator 
ls.coef <- lm(Success~Temperature)$coef
prob.ls <- exp(ls.coef[1]+ls.coef[2]*Temperature)/(1+exp(ls.coef[1]+ls.coef[2]*Temperature))

# Wald’s test is often used to test the significance of logistic regression coefficients
```

## 4.4 survival analysis
```r
# fit one line for the whole model
KM.model <<- survfit( Surv( time = SurvivalDays, event = IsNotCensored ) ~ 1 )
# fit lines for each level of ClinicNumber
KM.model <<- survfit( Surv( time = SurvivalDays, event = IsNotCensored ) ~ ClinicNumber )
print( summary( KM.model ) )
```

## 4.5 Anova, two sample t-test, linear regression
The mean responses (and thus the random error terms) of all three models are identical. All three models describe two populations with the same variances, but possibly different means. In each model, the assumptions about the random errors are the same (normal with mean zero and variance. 2 ). Thus, the p-value must also be identical for all three models. It is not obvious why the square of a t-distributed statistic should have an F-distribution (a proof of that requires a bit of statistical theory), but when the model assumptions are the same, it is comforting that either test statistic provides the same p-value.

## 4.6 Random sampling & allocation
 Random sampling (selecting units randomly from a larger well-defined population) is not the same as random allocation (randomly assigning treatments to units).

 Random sampling and random allocation can be used to convert unplanned systematic variability into random variability. For example, in the game study, the subjects’ natural ability may bias the results if more talented subjects tend to play one game type over the other. However, if we randomly allocate subjects to a game type, we can expect each group to have an equivalent number of talented subjects. In addition, the variability in natural abilities now tends to look like the random variability that can be modeled with the error term.
 
 
 ## 4.7 Simulation for p-value
```r
reps <- 10000
results <- numeric(reps) 
cancer.cells <- c(rep("M",24),rep("B",13))

for (i in 1:reps) {
  results[i] <- sum(sample(cancer.cells,21, replace = FALSE)=="M")
  }
 sum(results>=17)/reps

or 

trails <- 10000
count <- sapply(1:trails, function(x){
  sum_m <-sum(sample(a,21, replace = FALSE))
    })

```

## 4.8 Model Selection
```r
with( df.corrected, {
    explanatories <- cbind( Age, Height, 
        Neck, Chest, Thigh, 
        Knee, Ankle, Biceps, Forearm, Wrist )
    exp.names <- c( "Age", "Height", 
        "Neck", "Chest", "Thigh", 
        "Knee", "Ankle", "Biceps", "Forearm", "Wrist" )
    leaps.result <<- leaps::leaps( explanatories, PCTBF, method = "adjr2", names = exp.names, nbest = 2 )
    cat( "Size", "AdjR2", exp.names, sep = "\t" )
    cat( "\n" )
    sapply( 1:length( leaps.result$size ), function( i ) {
        cat( leaps.result$size[ i ],
            round( leaps.result$adjr2[ i ], digits = 3 ),
            leaps.result$which[ i, ], "\n", sep = "\t" ) } )
} )


require(leaps)
full.data=cbind(Cars$Mileage,Cars$Cyl,Cars$Liter,Cars$Doors,Cars$Cruise,Cars$Sound,Cars$Leather)

best.lm <- leaps(full.data,Cars$Price, method = "adjr2", names =c('Mileage','Cyl','Liter','Doors','Cruise','Sound','Leather'), nbest=3)

data1 = cbind(best.lm$which,best.lm$adjr2)
```


