# Lab 2 Assignment

> Your lab was outsandingly thorough.

> Final Grade 18/20

## Part 1

1)	Your identifications (how many species do you recognize in the group, and which specimens belong to which species). Explain how and why you came to this conclusion.

+ “Mikey” Large, deep ribbing- 8, 1, 18/20, 11, 21
+ “Leo” Tight whorl- 16, 17/22, 19, 25, 5/14, 23, 
+ “Donny” Barely any ribbing- 7, 9, 4, 10, 13, 3, 15
+ “Raph” Symmetrical looking, slight ribbing- 12, 24, 6, 2

````R
> colMeans(Mikey)
  Specimen          D         UD         WD      Strat 
13.1666667 49.9666667  0.4283333  0.2500000  8.7000000 
> colMeans(Leo)
Specimen        D       UD       WD    Strat 
 17.6250  39.3125   0.3075   0.2525   4.3250 
> colMeans(Donny)
  Specimen          D         UD         WD      Strat 
 8.7142857 41.7857143  0.3828571  0.2242857  6.3857143 
> colMeans(Raph)
Specimen        D       UD       WD    Strat 
 11.0000  18.1000   0.3875   0.2950   6.9000
#disregard the mean Specimen and Strat values
````

After looking at morphological characteristics and running the mean U/D ratio and mean W/D ratio each group has been segregated based on whorl shape, ribbing, and these ratios. Upon further investigation, each mean umbilical width to diameter ratios are unique enough to mark different species. Species Donny and Ralph have similar U/D and W/D ratios but are morphologically different enough in size and ribbing pattern so I grouped the smaller ammonites as one species.

> Well thought out, and you showed that you looked at the data. Excellent!

2)	The morphological features you used to distinguish each species, including whatever combination of qualitative or quantitative traits you think are important.

I first looked at morphological features to separate the ammonites into groups.  This was the easiest way to distinguish separate features such as having a tight whorl (so a small “U” value), ribbing characteristics, and how symmetrical the shell looked (so how “circular” it was and how symmetrical the whorl was).  I then looked at the smaller ammonites and grouped any that looked similar to the larger shells in the corresponding group.  Any shell that looked like a juvenile form of another is denoted above by a “/” (i.e. species 18 is the juvenile form of 20).

3.	The nature of ontogenetic change, if any, in the species. Explain your reasoning.

Any ontogenetic changes present in these species I have identified as paedeomorphic and I mostly looked at size and ribbing pattern changes.  After looking at the ribbing patterns first, any ammonites with similar patterns were grouped together no matter what size they were so with the retention of ribbing patterns throughout genera, this would correspond to a paedeomorphic classification of ontogenetic change. This is most apparent in the grouping Leo that I made based on having a tight whorl (or small “U” value) since they are a variety of sizes but maintain similar forms.

4.	The possibility of sexual dimorphism as a cause of morphological differences and how you evaluated that possibility.

> I think you knew, but you do not clearly state that male ammonites are generally thought to be slightly smaller than females. -0.25.

Some of the shells look very similar in ribbing patterns so I figured shells that were close in size with similar ribbing would be a male/female dichotomy represented.  For example, shells 3 and 15 look almost identical but 15 has a slightly tighter whorl but have a similar cracked pattern with minimal ribbing.

## Part 2-1

1)	Each element of the plethodon list has a name. What are they?

Land, links, species, site, outline

2)	What class is each object?

Array, matrix, factor, factor, matrix

3)	Whare are the dimensions of the first object in the plethodon list?

12 by 2 by 40

## Part 2-2

1)	Use the hummingbird dataset. Which object in the list records the landmark data?

````R
>names(Hummingbirds)
#the first object is landmark data (“land”)
````

2) Perform a procrustes on the landmark data.

````R
> ProcrustesHummingbirds<- gpagen(hummingbirds[["land"]])
````

4.	 Perform a PCA on the hummingbird data.

````R
> plotTangentSpace(ProcrustesHummingbirds[["coords"]],warpgrids=FALSE,verbose=FALSE)
````

5.	How many "species" of hummingbird are there?

> You did not explain why you thought this? -1 point

There could be 2-4 different “species” of hummingbird

## Part 3

1)	What is the synapomorphy of the clade containing species D and E?

Fangs longer than 6 inches

2)	What is a plesiomorphic character of that clade?

Sulfurous odor

3)	What is the synapomorphy of the clade containing species A and B?

Adorable eyelashes

4)	Which taxa have a sulfurous odor?

C, D, E

5)	What character distinguishes species D from species E?

Presence of a laser death ray in species E

6)	Are adorable eyelashes a synapomorphy or an autapomorphy? 

<strike>Autapomorphy</strike> Synapomorphy
> -0.5 points

7)	Traditionally, the five taxa are grouped into three families. Determine if each family is monophyletic, paraphyletic, or polyphyletic.

+ Family 1 is monophyletic 
+ Family 2 is <strike>paraphyletic</strike> polyphyletic
+ Family 3 is monophyletic

> - 0.25 Points

8)	More recently, species A has been grouped in a family with species D and E. Is this advisable? Why or why not?

No, this would then make the family a paraphyletic group and the common trait that the three species share isn’t even detailed on the tree so we don’t know how far back the MRCA is for these species.

9)	Determine if the following groups are monophyletic, paraphyletic, or polyphyletic. 
	
Group | Species | Classification
----- | ----- | -----
Group 1	| Species A, B, C. | Paraphyletic	
Group 2	| Species C, D, E. | <strike>Monophyletic</strike> polyphyletic
Group 3	| Species C and D. | <strike>Polyphyletic</strike> paraphyletic	
Group 4	| Species A and B. | Monophyletic	
Group 5	| Species B, D, E. | <strike>Paraphyletic</strike> polyphyletic	

> - 0.75 points

## Part 4

1)	Assuming that *Gryphaea arcuata* represents the ancestor, what type of heterochrony is most likely responsible for evolution of these two species? 

This trajectory of evolution exhibits peramorphosis.  Species D and E are larger and wider than *Gryphaea arcuata* but retain the adult characteristics seen in (C).

> 0.25, *G. gigantea* indicates paedomorphosis.
 
2.	Which species of *Gryphaea* has undergone a greater degree of heterochrony?

*Gryphaea gigantea* has undergone a greater degree of evolution and heterochrony because it has widened and grown in size compared to *Gryphaea arcuata* and has a modified paedomorphic characteristic of the side-view that is similar to the juvenile A stage.

3.	What type of heterochrony is represented in the *Ollenus* example??

From *Ollenus lapworthi* through *Ollenus* intermedius, there is a retention of gradual exhibition of more “adult” characteristics.  But the speciation event that led to the appearance of *Ollenus armatus* caused a more extreme phenotype that mirrors the ontogenic ancestor of *Ollenus lapworthi* so this could be considered a retention of juvenile characteristics so this would be paedomorphic heterochrony.

