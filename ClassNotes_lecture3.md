# Lecture 3

Chosing metrics for an A/B test

## Metrics of an A/B test

1. Invariant metrics - metrics that do not change value in control and expt
2. evaluation metrics
    i. High level business metrics
    ii. User experience metrics

Some evaluation metrics may take too long to collect or the data for that metric may not be available. In that case we can use some proxies:

1. User Experience Research (UER)
2. External data
3. Focus group
4. Survey data
5. Retrospective analysis
6. Experiments

### Steps to selecting metrics for an experiment

1. Define problem and suitable metrics
2. Build intuition - measure the change between control and expt & the variability of the metric
3. Characterize

#### Defining a metric

There are a number of ways we can calculate a given metric once we have defined it. For instance for a metric like "click through probability" which is defined as

    CTP = # clicks / # users that visit the page

the # users that click the page can be defined in a number of ways. 

##### 1.By Interval

Number of Users/Cookies cick in a given "session". Where session is defined by a fixed amount of time for instance 1 day or 12 hours or 1/2 hour.

##### 2.By Pageview

Instead of counting number of cookies/users that click we can also get the success rate through # of pageviews with clicks in them thereby calculating the proportion of PVs with clicks

##### 3.Calculating rates

Calculate just the total number of clicks and divide by total pageviews. This would be a rate and not a probability.

All three of these metrics would have different values and the #1 would have different values also depending on the time interval chosen. Best way to chose which metric to use and the specific details therein is to slice the data to get the best definition.

#### How to chose a metric

Things to keep in mind when selecting a metric:

1. Sensitivity - how sensisitve is the metric in detecting the change
2. Robustness - how robust is the metric against changes in we don't want to test

    * A way to test robustness is to run a A/A test where we measure the metric between 2 groups without any change to see the variability in the metric

3. Distribution of the metric - capture through retrospective analysis
4. Categories of metrics:

    * Sums, counts
    * Distribution based - median, 25th percentile, 95th percentile
    * Probabilities and rates
    * Ratios

#### How to measure the change in the metric between the control and experiment

1. Simple: absolute difference between the control and experiment evaluation metric
2. Actual: See % change in the metric between control and experiment. This method is especially useful when we are running too many experiments and need to keep in context the changes in the system. Also helps when the system has seasonal changes. By using % change we just need one practical significance boundry to get stability over time.

#### Measuring the variability of a metric

We may or may not be able to calculate the analytical or emperical variability for data depending on the metric and the data distribution. In order to calculate the confidence interval analytically we need:

1. The variance
2. The underlying distribution of the data

For instance if we know that our data follows a binomial distribution we can calculate the standard error (sqrt of variance) as

SE = SQRT( P_hat * (1-P_hat) / N )

And assuming that the distribution has a large enough N (i.e. the sample size) to be considered equivalent to a normal distribution,
m = Z * SE

where m is the margin of error used to build the confidence interval and Z is the z-score for the xth% confidence boundry.

##### Some common type of metrics and their analytical distributions

| Type of Metric | Distribution | Estimated Variance |
|     :---:      |     :---:    |     :---          |
| probability    | Binomial (Normal with large N) | P_hat*(1-P_hat)*1/N |
| Mean | Normal (Central limit theorem) | Sigma^2/N where Sigma squared id the variance of the sample |
| Count/Difference | Normal (not always but mostly) | Var(x)+Var(y) where x and y are the component metrics |
| rates | Poisson Distribution | Mu i.e. the sample mean |
| diff between rates | not poisson, not normal | variance of difference between 2 poisson distributions or Mu1 / Mu2 if it is close to 1 and calculate the variance of that |
| Ratios | Depends | Depeneds |