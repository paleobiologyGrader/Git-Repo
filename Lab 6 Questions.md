##Part 1

> Great job. 19/20

1)	As part of our matching procedure between the Macrostrat database and the Paleobiology database, we lost some data - i.e., there was some Paleobiology Database occurrences that could not be matched to the Macrostrat database. How many occurrences were lost? Show your code.

````R
> dim(DataPBDB)
[1] 34166    26
> dim(MacroPBDB)
[1] 9013   13
````

There are 34,166 occurrences in DataPBDB but only 9,013 in MacroPBDB. 25,153 occurrences were lost.

2)	Using what you know about the Macrostrat database can you speculate as to why so much data was lost?

Since the Macrostrat database is only data from North America there is probably a lot of data from the Cambrian period that occurs outside of North American formations that is included in DataPBDB.

##Part 2

1)	A good candidate for classification as a lagerstätten should have high diversity of different taxnomic orders. Calculate the order-level richness of each stratigraphic formation. Find the top 10 candidate units by this criteria. State them and give the code you used. Also, create a character vector( ) listing the names of these stratigraphic units. Name this vector CandidateUnits.

````R
>OrderRich<- apply(OrderMatrix,1,specnumber)
>sort(OrderRich)
#Orders with the highest richness
Forteau Fm                             Parker Slate                           Snowy Range Fm 
    14                                       16                                       16  
Weymouth Fm                              Langston Fm                            Wheeler Shale 
    16                                       17                                       18 
 Marjum Limestone                               Stephen Fm                               Kinzers Fm 
       19                                     		  23                                       24 
   Chancellor 
      27

> CandidateUnits<- c("Forteau Fm", "Parker Slate", "Snowy Range Fm", "Weymouth Fm", "Langston Fm", "Wheeler Shale", "Marjum Limestone", "Stephen Fm", "Kinzers Fm", "Chancellor")
````

2) A good candidate for classification as a lagerstätten should have a large number of genera that are relatively rare. Using the GenusMatrix column to find out how many samples each genus occurs in. Show the code you used. Name your output GenusFrequencies.

````R
> GenusFrequencies<-colSums(GenusMatrix)
````

3) What is the necessary code to make a frequency barplot of the GenusFrequencies?

````R
> barplot(table(GenusFrequencies))
````

4) After looking at this barplot, you should see a familiar paleobiological pattern. What do we call this type of curved distribution in paleobiology and ecology. [Hint: Think back to the lectures]

This barplot follows a hollow curve pattern.

5) Subset your new vector GenusFrequences so that only those genera from the lower 50% of the distribution are present. In other words genera with occurrences <= to the median( ). Show your code. Name this new subset vector as RareGenera.

````R
> RareGenera<- c(which(GenusFrequencies<=median(GenusFrequencies)))
````

> This was incomplete -1 Points

##Part 3

1)	Subset GenusMatrix so that it only shows the 10 stratigraphic units we determined were potential candidates. Show your code and name your new matrix, CandidateMatrix.

````R
> CandidateMatrix<- GenusMatrix[CandidateUnits, ]
````

2) Based on the output of PercentShared and your answer to Problem Set 2 - Question 1 - i.e., the ranking of candidate units based on the number of orders represented, which four units do you think are most likely to qualify as Lagerstätten? Explain your reasoning.

````R
> percentRare<-function(CandidateUnit,RareGenera) {
+     CandidateUnit<-CandidateUnit[CandidateUnit>0] 
+     PercentIn<-length(which(names(CandidateUnit) %in% names(RareGenera))) 
+     TotalGenera<-length(CandidateUnit) 
+     PercentShared<-PercentIn/TotalGenera
+     return(PercentShared)
+ }
> PercentShared<-apply(CandidateMatrix,1,percentRare,RareGenera)
> PercentShared
      Forteau Fm     Parker Slate   Snowy Range Fm      Weymouth Fm      Langston Fm    Wheeler Shale 	Marjum Limestone 
   0.5652174        0.2812500        0.1951220        0.6764706        0.1632653        0.2307692        0.3559322 
      Stephen Fm       Kinzers Fm       Chancellor 
       0.3055556        0.2586207     0.5714286

#Forteau Formation, Weymouth Formation, Chancellor, and Marjum Limestone are most likely to be a Lagerstatten.
````

3)Look closer into the into the four units you chose - using Google and information in the Paleobiology Database. One of these should be a very famous Lagerstätten. Which one? What is famous about it? What is its significance to Paleobiology?
The Chancellor Peak in Canada is part of the Burgess Shale formation where a rare cactus, Chancelloria eros, is found. Fossils found in this area are very rare and from the Middle Cambrian period. The Burgess Shale is famous for the preservation of soft parts of fossils and the completeness of the fossil record in this area.
