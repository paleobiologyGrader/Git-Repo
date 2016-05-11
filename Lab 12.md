> 20/20

## Part 1

Question 1
Download four data sets from the paleobiology database. First, a dataset of Anisian-Rhaetian Synapsids, name it TriassicSynapsids. Second, a dataset of Anisian-Rhaetian Diapsids, name it TriassicDiapsids. Third, a dataset of post-Triassic Diapsids, name it JurassicDiapsids. Fourth, a dataset of post-Triassic Synapsids, name it JurassicSynapsids. Show your code.
````R
 TriassicSynapsids<-downloadPBDB("Synapsida","Anisian","Rhaetian")
 TriassicDiapsids<-downloadPBDB("Diapsida","Anisian","Rhaetian")
 JurassicDiapsids<-downloadPBDB("Diapsida","Jurassic","Neogene")
 JurassicSynapsids<-downloadPBDB("Synapsida","Jurassic","Neogene")
 TriassicSynapsids<-cleanRank(TriassicSynapsids, "genus")
 TriassicDiapsids<-cleanRank(TriassicDiapsids, "genus")
 JurassicSynapsids<-cleanRank(JurassicSynapsids, "genus")
 JurassicDiapsids<-cleanRank(JurassicDiapsids, "genus")
````

Question 2
````R
How many Diapsid genera were there in the Triassic dataset? How many Synapsid genera? Show your code.
 TriassicDiapsids<- unique(TriassicDiapsids [,"genus"])
 TriassicSynapsids<- unique(TriassicSynapsids [,"genus"])
 length(TriassicDiapsids)
[1] 389
 length(TriassicSynapsids)
[1] 116
````

Question 3
How many Triassic Diapsid genera survived the Triassic/Jurassic transition? How many were victims? How many Triassic Synapsid genera survived the Triassic/Jurassic Transition? How many were victims? Show your code.

````R
 JurassicSynapsids<- unique(JurassicSynapsids [,"genus"])
 JurassicDiapsids<- unique(JurassicDiapsids [,"genus"])
 SynapsidSurvivor<- intersect(TriassicSynapsids, JurassicSynapsids)
 SynapsidVictim<- setdiff(TriassicSynapsids, JurassicSynapsids)
 DiapsidSurvivor<- intersect(TriassicDiapsids, JurassicDiapsids)
 DiapsidVictim<- setdiff(TriassicDiapsids, JurassicDiapsids)
 length(SynapsidSurvivor)
[1] 9
 length(SynapsidVictim)
[1] 107
 length(DiapsidSurvivor)
[1] 37
 length(DiapsidVictim)
[1] 352
````

Question 4

````R
Calculate the odds ratio and log-odds that Diapsid genera were more likely to survive the T/J transition than Synapsids.
 SynapsidOdds<- (length(SynapsidSurvivor)/length(TriassicSynapsids)) / (length(SynapsidVictim)/length(TriassicSynapsids))
 DiapsidOdds<- (length(DiapsidSurvivor)/length(TriassicDiapsids)) / (length(DiapsidVictim)/length(TriassicDiapsids))
 OddsRatio<- DiapsidOdds/SynapsidOdds
 OddsRatio
[1] 1.249684
 log(OddsRatio)
[1] 0.222891
Question 5
Using a 95% confidence interval, can you say that this odds/ratio is "statistically significant"? Show your code.
 StandardError<-sqrt(1/length(SynapsidSurvivor) + 1/length(SynapsidVictim) + 1/length(DiapsidSurvivor) + 1/length(DiapsidVictim))
 StandardError
[1] 0.3877175
 UpperLimit<-log(OddsRatio) + (StandardError*1.96)
 UpperLimit
[1] 0.9828172
 LowerLimit<-log(OddsRatio) - (StandardError*1.96)
 LowerLimit
[1] -0.5370353
# The lower interval is negative so we cannot say that this is statistically significant.
````

## Part 2

Queston 1
Download a dataset of Anisian-Rhaetian Diapsids and Synapsids, and a dataset of post-Triassic Diapsids and Synapsids. Show your code.

````R
 TriassicAll<- downloadPBDB(c("Diapsida", "Synapsida"), StartInterval = "Anisian", StopInterval = "Rhaetian")
 PostTriassicAll<- downloadPBDB(c("Diapsida", "Synapsida"), StartInterval = "Jurassic", StopInterval = "Neogene")
 TriassicAll<- cleanRank(TriassicAll, "genus")
 PostTriassicAll<- cleanRank(PostTriassicAll, "genus")
````

Question 2

````R
Find the mean latitude of each genus's occurrences in your Triassic dataset. Show your code.
 MeanLatitudeTriassic<-tapply(TriassicAll[,"paleolat"],TriassicAll[,"genus"],mean)
Question 3
Find which Triassic genera were survivors and which were victims of the Triassic/Jurassic event. Show your code.
 TriassicSurvivors<-subset(TriassicAll,TriassicAll[,"genus"]%in%unique(PostTriassicAll[,"genus"])==TRUE)
 TriassicSurvivors<-unique(TriassicSurvivors[,"genus"])
 TriassicVictims<-subset(TriassicAll,TriassicAll[,"genus"]%in%unique(PostTriassicAll[,"genus"])!=TRUE)
 TriassicVictims<-unique(TriassicVictims[,"genus"])
````

Question 4
Find which genera of your Triassic dataset were Diapsids and which were Synapsids. Show your code.

````R
 Victims<-array(0,dim=length(TriassicVictims),dimnames=list(TriassicVictims))
 FinalMatrix<-merge(MeanLatitudeTriassic,Victims,all=TRUE,by="row.names")
 FinalMatrix<-transform(FinalMatrix,row.names=Row.names,Row.names=NULL)
 colnames(FinalMatrix)<-c("MeanLatitudes","Survivor/Victim")
 FinalMatrix[is.na(FinalMatrix[,"Survivor/Victim"]),]<-1
````

Question 5

````R
Perform a logistic regression where the outcome variable is Survivor/Victim and the input variable is the mean latitude of each genus. Show your code. Was the mean latitude of a Triassic genus a good predictor of its survival across the T/J extinction?
 Regression<-glm(FinalMatrix[,"Survivor/Victim"]~FinalMatrix[,"MeanLatitudes"],family="binomial")
 summary(Regression)
Call:
glm(formula = FinalMatrix[, "Survivor/Victim"] ~ FinalMatrix[,
    "MeanLatitudes"], family = "binomial")

Deviance Residuals:
    Min       1Q   Median       3Q      Max  
-0.4474  -0.4411  -0.4385  -0.4308   2.1889  

Coefficients:
                                 Estimate Std. Error z value Pr(>|z|)    
(Intercept)                    -2.3009122  0.1547326  -14.87   <2e-16 ***
FinalMatrix[, "MeanLatitudes"]  0.0007725  0.0051555    0.15    0.881    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 308.10  on 504  degrees of freedom
Residual deviance: 308.08  on 503  degrees of freedom
AIC: 312.08

Number of Fisher Scoring iterations: 5

#The “Estimate” value is 0.0007725 so for every one degree of latitude, the likelihood of survival (based on the log odds) increases by 0.0007725 so genera in northern hemispheres have a very low odds ratio for survival so this is not a good predictor of surviving because the difference between surviving and going extinct at this border is so small with this measure. The p value is also very large so these calculations are also not statistically significant. 
````
