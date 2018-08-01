## Hypothesis Test

## Z statistics

z = (mu_X - mu_x) / (sigma / sqrt(n))

reject when sample difference is greater or number of observations is greater


## Type I and II Errors

I: when you reject a null hypothesis taht is in fact true;  (prob = alpha)

II: when you accept a null hypothesis that is in fact false; (prob = beta)

power of the hypothesis = 1- beta


## test when we know sigma

using z statistics and the sigma is the known sigma

z is in N(0,1)

so P(z > z0) can be calculated.

crit.0.95 = 1.64 so z > 1.645 should be rejected.


p-value = 1 - norm.s.dist(z, true)

in R it should be 1 - pnorm(z)


## test when we don't know sigma

in reality, it's more useful.

using  sample standard deviation as s

summation((x-mu_x)^2) = sigma^2

calculate the t statistics t = (mu_X - mu_x) / (s / sqrt(n))

t is in tDF distribution, where DF is degree of freedom


## hypothesis testing for the population proportion p










