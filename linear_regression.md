# Simple Linear Regression

```r
data(airquality)
names(airquality)

#[1] "Ozone"   "Solar.R" "Wind"    "Temp"    "Month"   "Day"

plot(Ozone~Solar.R,data=airquality)

#calculate mean ozone concentration (na´s removed)
mean.Ozone=mean(airquality$Ozone,na.rm=T)

abline(h=mean.Ozone)

#use lm to fit a regression line through these data:

model1=lm(Ozone~Solar.R,data=airquality)

model1

abline(model1,col="red")
plot(model1)

termplot(model1)
summary(model1)

```
