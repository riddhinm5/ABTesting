# Lecture 1

### Steps to set up an A/B test

1. Decide on change
2. Chose a Metric
3. review statistics (observational)
4. Design the test
5. Analyze results

### Kind of questions A/B testing can answer

* A/B testing cannot be used to ask general questions like is my site complete. A/B testing as described by some Silicon Valley VCs can tell you if you are going "up" a hill it can't tell you which of a new hill to climb
* Cannot use A/B testing for a brand new feature because
    1. There is no baseline metrics to test the new feature against in order to state an "improvement"
    2. There may be a novelty effect causing a larger than normal engagement as users explore the feature

* Best siuted for testing <b> existing features which need to be improved </b>
* pair A/B testing with backward testing to come up with a hypothesis

Usually for a usability test, rate is a good metric to chose for the test and for impact probability is a better metric

### A/B testin ==> Hypothesis testing

A/B testing is basically like hypothsis testing that is taught in any descriptive stats course [like](https://www.youtube.com/watch?list=PLkIselvEzpM7Pjo94m1e7J5jkIZkbQAl4&v=NVbPE1_Cbx8)


Setting up a hypothesis test with 2 samples to test a change, we will call the 2 samples control (where no change is made) and experiment (where the desired change is made). Let us assume the change being measured is the number of visitors who will click on a link when they visit a particular website. The hypothsis we will want to reject i.e. the null hypothsis is, 

H_o => the difference in probability between experiment and control is 0

and the alternative hypothsis is,

H_a => the difference between the probability in the experiment and control groups is non-zero

* Let X_cont be the number of users who click on the link from the control group
* Let X_expt be the number of users who click on the link from the experiment group
* Let N_cont be the number of users who visit the website from the control group
* Let N_expt be the number of users who visit the website from the experiment group

If the evaluation metric we are going to use is the probability of a click given visit to the page i.e. X/N the,

P_hat_pool i.e. the pooled probability is,

    > P_hat_pool = (X_cont + X_expt) / (N_cont + N_expt)

SE_hat_pool i.e. the standard error in the pooled probability is,

    > SE_hat_pool = SQRT(P_hat_pool * (1 - P_hat_pool) * (1/N_cont + 1/N_expt))

Also m, the margin of error can be given by,

    > m = Z_score * SE_hat_pool

Here the Z_score is the value that can be looked up in the [z-score table](http://www.z-table.com/) which helps us build a confidence interval with a x% decision boundry. For example if chose to have a decision boundry of 95% i.e. we are ok to chose the value of P such that 95% P's value will fall into the confidence interval we build.

d_hat i.e. the difference in the probability for the control group and the experiment group is,

    > d_hat = P_hat_expt - P_hat_cont

as with any metric there is a variability associated with the probability to click, this is captured in the SE measure. therefore when we try to evaluate the difference between the the probability in control vs. experiment we must consider if [d_hat - m, d_hat + m] is a range which does not include 0. if it does not we can say the change in probability is statistically significant and we can reject the null hypothsis.

Statistical signinficance however is not enough for making a decision for shipping a new feature. It is also important to keep a practical significance boundry. i.e. a minimum change we would like to see in the metric which would make business sense to make the change.

### Errors in hypothesis testing

There are 2 main error types in hypothesis testing Type I error also called alpha, and Type II error also balled Beta. Also important to keep in mind is 1-beta is also called sensitivity. 

<u>Definitions</u>
alpha = error which arises with the *incorrect rejection* of the null hypothsis . i.e. in the absense of an practical significance boundry, we accept there was a change in the metric even though there wasn't a statistically significant change

beta = error which arises with the *incorrect retaining* of the null hypothsis i.e. we accept that there is no significant change in the metric even though there actually is

therefore sensitivity is a measure to figure out if we are making sure we detect a change reliably when there is one. To increase the sensitivity we have to increase the number of pageview for the control and expt. With fewer pageviews we are more likely to accept the null hypothsis for small changes.
