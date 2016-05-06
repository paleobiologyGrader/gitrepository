## Problem Set 1

> 19/20

1) What do the max_ma and min_ma columns of DataPBDB represent? If you do not intuitively know, you can always check the Paleobiology Database API documentation.
+ Max_ma shows records whose temporal locality is at least _____ old in millions of years
+ Min_ma shows records whose temporal locality is at most _____ old in millions of years

2) What is oldest age of each genus? [Hint: Use the tapply( ) and max( ) functions we've used in previous labs]. Show the code you would use to find out.

`> tapply(DataPBDB[,"max_ma"],DataPBDB[,"genus"], max)`

3) What is the youngest age of each genus? [Hint: Use the tapply( ) and max( ) functions we've used in previous labs]. Show the code you would use to find out.

`> tapply(DataPBDB[,"min_ma"],DataPBDB[,"genus"], min)`

4) Find which genus has the most occurrences in the dataset [Hint: Use the table( ) function!]. What code did you use?

````R
thing<-sort(table(DataPBDB[,"genus"]))
> dim(thing)
[1] 1018
> thing[1018]
Anadara 
   1916 
````

5) What is the stratigraphic range of this taxon (i.e., your answer to question 4). Show your code.
66 Ma

````R
Anadara<-subset(DataPBDB, genus="Anadara")
> max(Anadara[,"max_ma"])
[1] 66
> min(Anadara[,"min_ma"])
[1] 0
````

## Problem Set 2
1) Qualitatively describe what is happening in the following line of code. A good answer should identify what the different arguments are for each function, and what they are used for.

`mean(sample(Lucina[,"paleolng"],length(Lucina[,"paleolng"]),replace=TRUE))`

finds mean paleolong of Lucina….

Lucina[,”paleolng”] : vector where data originates
Length(Lunina[,”paleolng”]) : positive number, the number of items to choose from
replace=TRUE : the numbers used can be used more than once
Sample : takes a sample of the data in the size specified from the element specified 
Mean : finds mean of the data

2) Plot a kernel density graph of ResampledMeans. Show your code. Does the distribution look approximately Gaussian? Explain why you think it does or does not.

`> plot(density(ResampledMeans))`

Yes, it looks to be approximately a normal curve! The mean is close to the middle of the distribution, and is fairly symmetric.

3) Find the mean of ResampledMeans, is it similar to the mean of the original data?
````R
> mean(ResampledMeans)
[1] 24.16227
OriginalMean
[1] 24.1997
````

They are very similar. 

4) Sort ResampledMeans from lowest to highest. [Hint: We learned how to sort a vector in Lab 6].

`> sort(ResampledMeans)`

5) Now that you have sorted ResampledMeans, what is the 2.5th percentile of ResampledMeans and what is the 97.5th percentile of Resampled means. If you do not know what a percentile is, or how to calculate it, you can use google. Show your code.

````R
> quantile(sort(ResampledMeans), c(.025, .975))
    2.5%    97.5% 
21.82094 26.28630 
````

6) Incidentally, these numbers (your answer to question 5) are the lower and upper confidence interval of the mean! Qualitatively explain why this is the case.

We took out the lower 2.5% of the data as well as the upper 97.5% of the data, leaving the last 95% of the data intact. So with the data that is left, there is a 95% probability that the mean will be present. 


## Problem Set 3

1) Based on the confidence intervals given above, do you think it likely or unlikely that Lucina is still alive?
It is likely that Lucina is still alive. The estimated extinction is between now and sometime in the future. 

2) Find the extinction confidence interval for the genus Dallarca. Show your code.

````R
> Dallarca<-subset(DataPBDB,DataPBDB[,"genus"]=="Dallarca")
> estimateExtinction(Dallarca[,"min_ma"],0.95)
Earliest   Latest 
 2.58800 -3.88749 
````

3) A pure reading of the fossil record says that Dallarca went extinct at the end of the Pliocene Epoch. Based on its confidence interval, do you think it is possible that Dallarca is still extant (alive)?

Based on the confidence interval, theres a chance it could still be extant. The end of the Pliocene was only 2.58 Mya and

4) In this case, should we trust the confidence interval or a pure reading of the fossil record? Explain your reasoning.

I think we should trust the confidence interval, because the geologic record is spotty and is missing many large chunks of time throughout the world. (And most of the rock record is deep beneath the surface, in places we are unable to obtain fossils.)

> But, if it was alive today, you don't think modern biologist would have discovered it? -0.5 points

## Problem Set 4

1) State one ecological reason why this assumption is unlikely to be true.

The assumption that fossils are evenly spread out is untrue because there are environments that are nearly impossible for organisms to live in. For example, there is a large biodiversity of organisms that live in reef environments, but only a few different organisms live in off shore areas with little sun light or a small amount of nutrients in the water (areas where only clay, and not sand, is deposited). 

2) State one geological reason why this assumption is unlikely to be true.

Organisms that are deposited in unconsolidated sediment on coastal shores are more likely to be disturbed and therefore more likely to not become fossilized. 

> this is an overly specific answer that doesn't realy convey an understanding of the broader point. -0.5 points


## Problem Set 5
1) How many occurrences are in DataPBDB. How many are in ExtantData? How many occurrences were lost by limiting our anaysis to only extant bivalves?

````R
> dim(DataPBDB)
[1] 67617    26
> dim(ExtantData)
[1] 59096    26
> 67617-59096
[1] 8521
````

2) How many unique( ) genera were in DataPBDB and ExtantData, respectively. Using this information, what percentage of Cenozoic bivalves in the PBDB are still extant today.

````R
> length(unique(DataPBDB[,"genus"]))
[1] 1018
> length(unique(ExtantData[,"genus"]))
[1] 532
> 532/1018
[1] 0.5225933
````

3) Find the stratigraphic range of fossil occurrences for each genus in the ExtantData dataset. If you do not remember how to do this, revisit Problem Set 1 of this lab.

````R
tapply(ExtantData[,"max_ma"],ExtantData[,"genus"], max)
tapply(ExtantData[,"min_ma"],ExtantData[,"genus"], min)
````

4) Using your answer to question 3, find which genera in ExtantData are not extant according to the PBDB - i.e., do not have a minimum min_age of zero. Show your code.

````R
tapply(ExtantData[,"min_ma"],ExtantData[,"genus"], min)!=0
which(last==TRUE)
last2<-which(last==TRUE)
names(last2)
````

6) Calculate the confidence interval for the extinction of the following genera (careful with your spelling!): Scrobicularia,Meiocardia, Dimya, Digitaria, Cuspidaria, Arctica, Aloides, Kurtiella, Gouldia, and Acrosterigma. Show your code. What percentage of these taxa have confidence intervals indicating that the taxon might still be extant?

````R
> Scrobicularia<-subset(DataPBDB,DataPBDB[,"genus"]=="Scrobicularia")
> estimateExtinction(Scrobicularia[,"min_ma"],0.95)
 Earliest    Latest 
  0.01170 -34.70966 
	
> Meiocardia<-subset(DataPBDB,DataPBDB[,"genus"]=="Meiocardia")
> estimateExtinction(Meiocardia[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -5.329574

> Dimya<-subset(DataPBDB,DataPBDB[,"genus"]=="Dimya")
> estimateExtinction(Dimya[,"min_ma"],0.95)
 Earliest    Latest 
 0.781000 -2.054688 

> Digitaria<-subset(DataPBDB,DataPBDB[,"genus"]=="Digitaria")
> estimateExtinction(Digitaria[,"min_ma"],0.95)
 Earliest    Latest 
 0.781000 -3.761154

> Cuspidaria<-subset(DataPBDB,DataPBDB[,"genus"]=="Cuspidaria")
> estimateExtinction(Cuspidaria[,"min_ma"],0.95)
 Earliest    Latest 
2.5880000 0.7771965

> Arctica<-subset(DataPBDB,DataPBDB[,"genus"]=="Arctica")
> estimateExtinction(Arctica[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -1.799104 

> Aloides<-subset(DataPBDB,DataPBDB[,"genus"]=="Aloides")
> estimateExtinction(Aloides[,"min_ma"],0.95)
Earliest   Latest 
   5.333     -Inf 

> Kurtiella<-subset(DataPBDB,DataPBDB[,"genus"]=="Kurtiella")
> estimateExtinction(Kurtiella[,"min_ma"],0.95)
 Earliest    Latest 
  0.01170 -34.70966 

> Gouldia<-subset(DataPBDB,DataPBDB[,"genus"]=="Gouldia")
> estimateExtinction(Gouldia[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -2.047386 

> Acrosterigma<-subset(DataPBDB,DataPBDB[,"genus"]=="Acrosterigma")
> estimateExtinction(Acrosterigma[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -3.481128 
````

90% of these taxa could still be extant today.
