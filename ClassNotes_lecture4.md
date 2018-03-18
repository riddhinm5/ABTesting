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