## Problem Set 1

> 13.75/20

You may not use vegan( ) for this subsection.

1) What is Bivalve generic richness in the Miocene? What code did you use to find out?

````R
table(BivalveAbundance["Miocene",])
sum(table(BivalveAbundance["Miocene",]))
sum(table(BivalveAbundance["Miocene",]))
[1] 2273
2273-1639
[1] 634
````

2) What is the Berger-Parker Index (The abundance of the most common species divided by the total abundance of all species) of Brachiopods genera in the Pliocene? What code did you use to find out? [Hint: the function max( ) may help you).

````R
> max(BrachiopodAbundance["Pliocene",])
[1] 22
> sum(BrachiopodAbundance["Pliocene",])
[1] 99
> 22/99
[1] 0.2222222
````

3) What is the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?

````R
1-sum((Abundances/Total number of individuals)^2)
(N) > sum(BrachiopodAbundance["Late Ordovician",])
[1] 6154
(n) Vector - BrachiopodAbundance[“Late Ordovician”,]
> 1-sum((n/N)^2)
[1] 0.9784588
````


4) What is the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?
Shannon’s Entropy:  -(sum((n/N)*(log(n/N))))

n: 
````R
> n<-BivalveAbundance["Late Cretaceous",BivalveAbundance["Late Cretaceous",]>0]
````

N: > 
````R
sum(BivalveAbundance["Late Cretaceous",])
[1] 29684

> -(sum((n/N)*(log(n/N))))
[1] 5.086654
````

5) What is the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?

Shannon’s Entropy:  -(sum((n/N)*(log(n/N))))

n: > 
````R
n<-BivalveAbundance["Paleocene",BivalveAbundance[“Paleocene",]>0]
````

N:
````R
N<-sum(BivalveAbundance["Paleocene",])
[1] 29684

> -(sum((n/N)*(log(n/N))))
[1] 4.511875
````

6) What is the percent change in Shannon's Entropy between the Late Cretaceous and the Paleocene? Can you think of any major events that happened between the Late Cretaceous and Paleocene that might be relevant to biodiversity? [Hint: Use google if you don't know.] Is this reflected in this index?

````R
> (5.086654-4.511875)/5.086654
[1] 0.1129975
````

11% change, Late K asteroid impact, huge decrease in biodiversity

7) What if you use the exp( ) function to exponentiate the Shannon's Entropies you calculated in questions 4,5, and 6 (i.e.,e^Shannon's Entropy)? What percent of diversity is gained/lost? Does this better reflect the change between the Late Cretaceous and Paleocene? Why or why not?

````R
> exp(4.511875)/exp(5.086654)
[1] 0.5628292
````

56% diversity is lost, this better reflects the change associated with the Late K asteroid impact.

> Is that how much diversity was lost or how much diversity was left? -0.5 points

## Problem Set 2
Install (if you have not already) and load the vegan package into R. Read the help file for the diversity( ) function - ?diversity or help(diversity). You must have already loaded the vegan package in order for it to run.

````R
1) Use the specnumber( ) function (also from the vegan package) to find Bivalve richness in the Miocene. What code did you use to find out?
> specnumber(BivalveAbundance["Miocene",])
[1] 634
````

2) Use the diversity( ) function to find the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?

````R
> diversity(BrachiopodAbundance, index = "simpson", MARGIN = 1, base = exp(1))["Late Ordovician"]
Late Ordovician 
      0.9784588 
````

3) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?

````R
> diversity(BivalveAbundance, index = "shannon", MARGIN = 1, base = exp(1))["Late Cretaceous"]
Late Cretaceous 
       5.086654
````

4) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?

````R
> diversity(BivalveAbundance, index = "shannon", MARGIN = 1, base = exp(1))["Paleocene"]
Paleocene 
 4.511875
````

## Problem Set 3

````R
> Bivalvevector<-specnumber(BivalveAbundance)
> Brachiopodvector<-specnumber(BrachiopodAbundance)
````

Now that you have the two vectors of richness values. Let us see if they are correlated. You can use the cor( ) function to find the correlation coefficient.

1) Is brachiopod richness positively, negatively, or un-correlated with bivalve richness? Show your code?

````R
> cor(Bivalvevector,Brachiopodvector)
[1] -0.2376513
````

No correlation

> Really? No correlation, or just a week correlation? -0.25 points

2) Is brachiopod biodiversity positively, negatively, or un-correlated with bivalve biodiversity when using the Gini-Simpson index? Show your code?

````R
> Brachdiversity<-diversity(BrachiopodAbundance, index = "simpson", MARGIN = 1, base = exp(1))
> Bivalvediversity<-diversity(BivalveAbundance, index = "simpson", MARGIN = 1, base = exp(1))
> cor(Brachdiversity,Bivalvediversity)
[1] -0.2624135
````

No correlation 

> -0.25 points

3) Looking just at changes in brachiopod richness through time, when did the greatest drop in brachiopod richness occur (i.e., between what two consecutive epochs)?
Pennsylvanian and Cisuralian
> 564-284
[1] 280

> -1 Points


Problem Set 4
1) Repeat the above steps, but for the BrachiopodAbundance community matrix. What is the standardized richness you got for brachiopods. Show your code.
> SampleAbundancesBrachiopod<-apply(BrachiopodAbundance,1,sum)
> SampleAbundancesBrachiopod[which(SampleAbundancesBrachiopod==min(SampleAbundancesBrachiopod))]
Pleistocene 
         63 
> StandardizedRichnessBrachiopod<-apply(BrachiopodAbundance,1,subsampleIndividuals,Quota=63)
> StandardizedRichnessBrachiopod[1:6]
    Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician 
            43.11             34.16             38.31             45.96 
  Late Ordovician        Llandovery 
            42.06             41.62 


2) How does the standardized brachiopod richness (previous question) compare to the unstandardized brachiopod richness from Problem Set 3? Show your code. Explain your reasoning. [Hint: Don't forget to put your biodiversities in temporal order]


> - 1 Points

3) Make a scatter plot of standardized brachiopod richness versus standardized bivalve richness. Make a second scatter plot of unstandardized brachiopod richness versus unstandardized bivalve richness. Compare and contrast the two plots. What are the differences or similarities? Does standardizing or not standardizing matter? Show your code and explain your reasoning in detail. [Hint: If you forgot how to plot, revisit the previous lab]

> -2 Points
 
4) Do you believe that there is any evidence in these analyses to support the idea that bivalves outcompeted brachiopods over time? Explain your reasoning.

> -2 Points
