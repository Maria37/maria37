## Lab 6
Maria Rochford

**Part 1**

Reproducing the maps.

The original data and the weights manager
![ogg.JPG](ogg.JPG)

Changing the permutations to 99999
![99999.JPG](99999.JPG)

We then clicked on the high high and low low to visualize the outliers.

Using the significance filter. Above the significance was p <0.05 >
Here it is p<0.01 >
![01.JPG](01.JPG)

Next action is to check the Bonferroni and the False Discovery Rate.

Here we have the cores of a cluster and their neighbors
![coresandneighbors.JPG](coresandneighbors.JPG)

Now here are the Univariate Local Geary Cluster Maps
![uniGeary.JPG](uniGeary.JPG)

Interpretation of Spatial Autocorrelation

High-High:
![highhigh.JPG](highhigh.JPG)

Low-Low:
![lowlow.JPG](lowlow.JPG)

Negative:
![neg.JPG](neg.JPG)

Implementation of Local Getis-Ord statistics
![LocalGstat.JPG](LocalGstat.JPG)

Implementation of the Getis-Ord statistics with significance filter.
![GstatSig01.JPG](GstatSig01.JPG)


**Part 2**

Using the Demographics fileset from the Vital Sign 2016, I chose to do an analysis on the Median Household Income and household size.

My first step was to run a Moran's I to find the correlation between average household size and the median household income.

![p2MoransI.JPG](p2MoransI.JPG)

This is negatively correlated. It is saying that the higher the Median Household Income is, the smaller the household size is. This makes sense because if a family doesn't have children than they have more time to work and more money.


**Part 3**

Now I am going to run a regression model comparing the same variables as before (Median Household Income and Household size).

![RegRep1.JPG](RegRep1.JPG)

Both the Lag and Error tests are significant so that means that I need to look at the Robust LM lag and error. I need to run a lag test because the significance is higher.

![RegRep2.JPG](RegRep2.JPG)

This result means that household size is not statistically significant. There are alot of other factors to consider in the relationship between household income and size. 
