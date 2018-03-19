# Lecture 5

Analyzing the results of an A/B test.

## Steps to Analyze results of an A/B test

1. Sanity Check
2. Choose single metric or multiple metrics
3. Calculate change
4. Check for statistical significance
5. Sign test - Positive/Negative change
6. Statistical significance of sign test

### Sanity test

Making sure there was nothing wrong with setting up the experiment.

1. Check the invariant metrics and see if they stay the same in A and B
2. Check the unit of diversion
3. Check filters to make sure A/B are not different
4. Check if data capture worked the way it was supposed to
5. Check if the sizes of A and B are similar

In case of a learning experiment which would involve the users learning about a new feature there would be a small increase/change at first followed by a ramp over time.

#### How to check if the difference in population size is within expectations

1. Compute the standard deviation of teh binomial distribution with the probability of 0.5 for auser being places in control or experiment randomly
2. Multiply the stdev * z-score to get the margin of error of the probability of being placed in either groups
3. Compute the confidence interval probability +/- m
4. check whether the current observed fraction is within the interval

In case of "invariance" ie the split is incorrect look at day by day data.

##### Still a problem

1. Talk to engineering team
2. Try slicing the data by various dimensions ro see if one stands out
3. Check age of cookies, does one of the groups have more new cookies?
4. Debug experiment setup
5. retrospective analysis - something endemic with the experiment and assumptions made may be causing this
6. Use post & pre periods - were the same changes present

### Single metric: Analyzing results

1. Calculate the difference
2. Calculate the SE for the metric
3. Check for sign test to see if the change was positive or negative. Check how many days was the change positive, construct a binomial probability distribution and calculate a p-value tosee if the probability of seeing the +ve sign change based on the number trials that are statistically significant

However in case we are using rates which follow a poisson distribution we cannot use above steps which require a binomial distribtuion.

In case we need to calculate the SE for the difference emprically, we can compute the SE analytical as:

SE-analytical = SQRT(1/(N_cont + N_expt)) * SE-emperical / (SQRT(1/# of PVs for emperical calc))

**Simpson's Paradox** could be causing issues with the results on the A/B data. Results may be difference by segment from ones calculated overall. In this case mau have to look at it from the segment level. this will happen when the # of users in different dims are split differently across control and experiment (Berkley Women's acceptance rates)

### Multiple metrics: Analyzing results

Chances of false positives increase, higher the alpha higher the chances of this happening.

Challenge: There could be one metric that can show significant change simply becaise of a larger number of experiments if we use many metrics, i.e. if we use many many metrics the chances on of them show a significant change is large, especially if we are running multiple experiments.

**How do we solve this?** We can do multiple runs to test across multiple slices of the data - change should not be repeatible unless it is actually there. Or can do a bootstrap analysis. Also check if the same metric pops up as stat sig everytime then there could be something with the metric causing this.

Solution: Use a higher confidence interval i.e. lower alpha.

#### Methods to calculate chances of getting false positive

**Method 1:** Assume independence among metrics and choose alpha such that,
alpha_overall = 1 - (1- alpha_individual)^n

Where n is the number of metrics.

**Method 2:** Benferroni condition. It's a simple method, makes no assumptions of independence, it's conservative and give alpha_overall atleast as small as specified. With this method,

alpha_individual = alpha_overall / n

*problem:* metrics that are correlated move at the same time so this may be too conservative a choice.

## Making the recommendation

1. Is the change statistically significant
2. What is the change actually doing
3. Is the change worth the effort, ROI

** Should always ramp-up change experiment for % traffic instead of just turning it on directly**