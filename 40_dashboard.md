<!-- Space: OP -->
<!-- Parent: Operational Readiness Review -->
<!-- Title: OPR - Dashboard -->

# Dashboard

- Quantities that do not go below zero (i.e. any timing or byte counter) should have the Y-axis set to zero. Failing to set this can cause dashboard software to create misleading graphs
- Logarithmic scales are useful for handling quantities with a wide range of magnitudes, but they are also easily misread by hasty or uninformed readers. Use them carefully and be sure to call attention to them with text where possible
- Always specify units on your graph, especially on the y-axis.
- Percentages are unitless, but are still scaled by a factor of 100, so mark them as a percentage
- Some quantities like load average are unitless (i.e. seconds per second). These do not, strictly speaking, need a unit label, but it is often more easiliy understood to label them with something like “seconds/second” that indicates how they are measured
- Where possible be sure to call attention to aggregations used in a panel in the title of the panel - e.g. is this a mean or a percentile of some kind? If this is averaged or bucketed over time, how long is the bucket?
- Your dashboard should provide basic information about what version(s) of a service you are running
- Pie chart or table of all versions runnin w/ count
- Table of what instances/pods are running non-majority versions TODO: put some promQL here
