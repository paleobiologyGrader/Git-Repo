##Part 1
1)	What is Bivalve generic richness in the Miocene? What code did you use to find out?
> table(BivalveAbundance["Miocene",])
#returns a table of number of genera with certain number of occurrences. There are 1639 genera with values of 0 in the Miocene.
> sum(table(BivalveAbundance["Miocene",]))
#returns 2273. This is the total number of genera reported in the Miocene
>2273-1639
#There are 634 total for genera richness 
2)	What is the Berger-Parker Index of Brachiopods genera in the Pliocene? What code did you use to find out? [Hint: the function max( ) may help you).
> max(BrachiopodAbundance["Pliocene",])
#22
> sum(table(BrachiopodAbundance["Pliocene",]))
#3107
>22/3107
# 0.007080785
3)	What is the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?
> sum(BrachiopodAbundance["Late Ordovician",])
#6154
> 1- sum(((BrachiopodAbundance["Late Ordovician",])/6154)^2)
 #0.9784588
4)	What is the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?
> n<-BivalveAbundance["Late Cretaceous",which(BivalveAbundance["Late Cretaceous",]>0)]
>N<- sum(BivalveAbundance["Late Cretaceous",])
> -sum((n/N)*log(n/N))
[1] 5.086654
5) What is the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?
> m<-BivalveAbundance["Paleocene",which(BivalveAbundance["Paleocene",]>0)]
> M<- sum(BivalveAbundance["Paleocene",])
> -sum((m/M)*log(m/M))
[1] 4.511875
6) What is the percent change in Shannon's Entropy between the Late Cretaceous and the Paleocene? Can you think of any major events that happened between the Late Cretaceous and Paleocene that might be relevant to biodiversity? [Hint: Use google if you don't know.] Is this reflected in this index?
>4.511875/5.086654
#returns 0.8871125 so there was about a 12% reduction in richness. This marks the difference in richness after the Cretaceous-Paleogene mass extinction event. But it is predicted that about ¾ of all species on Earth went extinct so there should have been a much greater reduction in richness than we see from the Shannon’s Entropy calculation. 
7) What if you use the exp( ) function to exponentiate the Shannon's Entropies you calculated in questions 4,5, and 6 (i.e., e^Shannon's Entropy)? What percent of diversity is gained/lost? Does this better reflect the change between the Late Cretaceous and Paleocene? Why or why not? 
> exp(-sum((m/M)*log(m/M)))
[1] 91.09244
#for Paleocene
> exp(-sum((n/N)*log(n/N)))
[1] 161.8474
#for Late Cretaceous
> 91.09244/161.8474
[1] 0.5628292

These values give a change in species richness of about 44% which is closer to the predicted loss of species richness due to the mass extinction.

##Part 2

1)	Use the specnumber( ) function (also from the vegan package) to find Bivalve richness in the Miocene. What code did you use to find out?
> specnumber(BivalveAbundance)
Miocene 
   634

2)	Use the diversity( ) function to find the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?
> diversity(BrachiopodAbundance["Late Ordovician",], index="simpson", MARGIN=1)
[1] 0.9784588
3) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?
> diversity(BivalveAbundance["Late Cretaceous",], index="shannon", MARGIN=1, base= exp(1))
[1] 5.086654
4) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?
> diversity(BivalveAbundance["Paleocene",], index="shannon", MARGIN=1, base= exp(1))
[1] 4.511875


##Part 3
Step1
> BivalveRich<- apply(BivalveAbundance,1,specnumber)
> BrachRich<- apply(BrachiopodAbundance,1,specnumber)

Step2
> BivalveRich<- BivalveRich[c("Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian","Lopingian","Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous","Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> BrachRich<- BrachRich[c("Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian","Lopingian","Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous","Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]

Step3

1)	Is brachiopod richness positively, negatively, or un-correlated with bivalve richness? Show your code?
> cor(BivalveRich, BrachRich)
[1] -0.567194
They are moderately negatively correlated.
2) Is brachiopod biodiversity positively, negatively, or un-correlated with bivalve biodiversity when using the Gini-Simpson index? Show your code?
> BivalveRich2<- diversity(BivalveAbundance, index="simpson", MARGIN=1)
> BrachRich2<- diversity(BrachiopodAbundance, index="simpson", MARGIN=1)

> BrachRich2<- BrachRich2[c("Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian","Lopingian","Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous","Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> BivalveRich2<- BivalveRich2[c("Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian","Lopingian","Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous","Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]

> cor(BivalveRich2, BrachRich2)
[1] -0.2355647

very loosely negatively correlated
3) Looking just at changes in brachiopod richness through time, when did the greatest drop in brachiopod richness occur (i.e., between what two consecutive epochs)? 
 The greatest change in richness is between the Lopingian and Early Triassic epochs (406 to 63).

##Part 4

1)	Repeat the above steps, but for the BrachiopodAbundance community matrix. What is the standardized richness you got for brachiopods. Show your code.
> SampleAbundances<-apply(BrachiopodAbundance,1,sum)
> StandardizedRichness<-apply(BivalveAbundance,1,subsampleIndividuals,Quota=124)
> BrachStandardizedRichness<- StandardizedRichness[c("Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> BrachStandardizedRichness
 Early Ordovician Middle Ordovician   Late Ordovician        Llandovery           Wenlock 
            42.00             36.70     	41.81             		37.54             45.88 
           Ludlow           Pridoli    Early Devonian   Middle Devonian     Late Devonian 
            43.19             35.08             51.75            	 35.74            		 33.27 
    Mississippian     Pennsylvanian        Cisuralian       Guadalupian         Lopingian 
            47.88             43.12            57.34             62.05             54.00 
   Early Triassic   Middle Triassic     Late Triassic    Early Jurassic   Middle Jurassic 
            28.02             53.75          64.28             57.64             61.50 
    Late Jurassic  Early Cretaceous   Late Cretaceous         Paleocene            Eocene 
            65.27             72.68         78.04             		63.28             72.61 
        Oligocene           Miocene          Pliocene       Pleistocene 
            76.47             86.69             85.30             84.21

2)	How does the standardized brachiopod richness (previous question) compare to the unstandardized brachiopod richness from Problem Set 3? Show your code. Explain your reasoning. [Hint: Don't forget to put your biodiversities in temporal order]
#The unstandardized brachiopod richness has much higher values than the standardized values. This is probably because the standardized values are based on a random sampling of a fixed number of brachiopods in the data set and each interval is sampled down to 124 individuals.
> BrachRich-BrachStandardizedRichness
 Early Ordovician    Middle Ordovician   Late Ordovician        Llandovery           Wenlock 
            99.00            245.30         289.19                233.46                 211.12 
           Ludlow           Pridoli    Early Devonian   Middle Devonian     Late Devonian 
           190.81            102.92            445.25            317.26         240.73 
    Mississippian     Pennsylvanian        Cisuralian       Guadalupian         Lopingian 
           266.12            240.88          	  506.66            486.95          	352.00 
   Early Triassic   Middle Triassic     Late Triassic    Early Jurassic   Middle Jurassic 
            34.98             57.25         128.72             72.36            113.50 
    Late Jurassic  Early Cretaceous   Late Cretaceous         Paleocene            Eocene 
            45.73             52.32         17.96          		  -34.28            -15.61 
        Oligocene           Miocene          Pliocene       Pleistocene 
           -46.47            -41.69            -62.30            -65.21
3) Make a scatter plot of standardized brachiopod richness versus standardized bivalve richness. Make a second scatter plot of unstandardized brachiopod richness versus unstandardized bivalve richness. Compare and contrast the two plots. What are the differences or similarities? Does standardizing or not standardizing matter? Show your code and explain your reasoning in detail. [Hint: If you forgot how to plot, revist the previous lab]
> plot(x=BrachStandardizedRichness, y=BivalveStandardizedRichness)
> plot(x=BrachRich, y=BivalveRich)
Standardizing gives a plot that can be fitted with a linear trend line whereas the unstandardized Brachiopod richness vs. Bivalve Richness gives a plot that could be fit with a quadratic trend. Relationships are typically easier to analyze and deduce when there is a linear relationship to examine. The standardized data is also less clustered than the unstandardized data and would have a much better fit line.
3)	Do you believe that there is any evidence in these analyses to support the idea that bivalves outcompeted brachiopods over time? Explain your reasoning.
According to both plots it does not appear that bivalves outcompeted brachiopods. After looking at the unstandardized data it appears that bivalves outcompete brachiopods because high values of bivalves correspond to low values of brachiopods but high levels of brachiopods appear to correspond to lower values of bivalve richness.  Since this data is not as reliably fit by a trend line it is better to look at the standardized data for this relationship. Looking at the standardized plot, there is no evidence of either species outcompeting the other because of the linear trend.  

<a href="url"><img src="/Lab5Plots/Figure1.png"></a>

<a href="url"><img src="/Lab5Plots2/Figure2.png"></a>

