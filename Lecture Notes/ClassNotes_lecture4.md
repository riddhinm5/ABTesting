# Lecture 4

Designing an A/B test by making assumptions about the unit of diversion.

## Steps to design an experiment

1. Choose the subject
2. Choose the "population"
3. Calculate Size of both classes needed
4. Calculate the time the experiment needs to run

## Unit of Analysis & diversion

When we choose a subject for the experiment we also need to chose the unit of diversion i.e. what event to show the change to:

1. The user - need to consider ethical implications
2. A Pageview - need to make sure of consistent experience
3. Unique cookie
4. device id - can be used only in case of a mobile device
5. IP address - could be useful for more infrastructure type changes

The Unit of analysis is whatever the denominator of the metric we choose is going to be. the unit of analysis i.e. the denominator of the metric should be the same as the unit of diversion which is going to be used to meausre the nuemerator. If the unit of analysis and diversion are different the analytical SE value will be an overestimate, so better to move to the emperical variability calculation in such cases.

### Types of experiment

* Intra-user experiment

same user will be in the control and experiment. Can use this kind of an experiment where there is no change in the user experience like change of ranking. 

* Interleaved experiment

Show both A and B at the same time, also applicable for ranking experiments

* Inter-user experiment

Has different users on the A & B sides. Can make it more segmented with cohorts by targeting this experiment to just the traffic from that cohort if we know the change will effect or be seen by that cohort alone. However, filtering can change the variability of the metric. Should keep this in mind, when calculating baseline.

It's usually not beneficial to use cohorts unless absolutley necessary, as we are reducing the number of users we can show the change to leading to increase in amount of time we will need to run the experiment.

Cohorts can be used when:

1. Looking for a learning effect
2. Examining user retention
3. Measure Increased user activity
4. Anything requiring a "user" being established

### Sizing the experiment

* Should make the sizing decision first, before starting the experiment
* Should be followed by chosing unit of diversion
* Repeat 1 and 2 iteratively until ideal size and unit of diversion are found

### Duration of the experiment

Depends completely on the size of the experiment. Essentially # of PVs per unit of time / # of Pvs needed is the duration of the experiment. It also depends on the % of traffic which is directed to the experiment. Mostly, would not want to use 100% of the traffic to show the latest change because:

1. Security, test if everything is ok would not want a major crash
2. Press/Blog traffic may attract too much attention before the decision to launch is made and can make more harm than good
3. Holiday/Weekend behavior is different, so change may be positive simply because of timing, cannot isolate if timing was cause of success/failure or the actual feature. Also if released at the time of a holiday may cause a lot of confusion and bad publicity if the new change is not good
4. A large site may have many different tests running simultaneously with different parameters