> 20/20

## Problem Set 1

1) You first mission is to download a list of all Triassic units in the Macrostrat Database using the /units route into R. Name this object TriassicUnits. As always, show your code.

`>TriassicUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Triassic&response=long&format=csv")`

2) How many Triassic units did you download? What code did you use to find out?

````R
> nrow(TriassicUnits)
[1] 838
````

3) Look at the first 10 units that you downloaded. Are they mostly Igenous, Metamorphic, or Sedimentary rocks? Do you believe that these units are relevant for an investigation of fossil preservation? Show your code and explain your reasoning.
````R
> SubsetTriassic<-TriassicUnits[(1:10),]
> SubsetTriassic[,"lith"]
````

These units are mostly Igneous rocks with a few Metamorphic. Igneous rocks are formed by lava flow so fossils are probably not preserved well and metamorphic rocks are created under high pressure so fossils will not be preserved in this condition either. So this data is not relevant to fossil preservation.

4) Which columns of your TriassicUnits data.frame denote the starting age and ending age of each unit, respectively?

“t_int_age” and “b_int_age” denote the ending and starting age, respectively.

5) Considering the bottom and top ages of the first 10 units, are these units constrained to only the Triassic or do some range through the Triassic?

````R
> SubsetTriassic[,"t_int_age"]
 [1]  66.0  72.1  89.8  89.8  89.8  89.8  93.9  93.9 100.5 100.5
> SubsetTriassic[,"b_int_age"]
 [1] 259.9 407.6 208.5 208.5 208.5 208.5 272.3 208.5 407.6 251.2
````

The Triassic spans from about 252 mya to 201 mya so all of these units range through the Triassic.


#Problem Set 2

1) Re-download TriassicUnits, however, this time restrict the data to only sedimentary rocks. Show your code.

`>TriassicUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Triassic&response=long&lith_class=sedimentary&format=csv")`

2) Restrict TriassicUnits to only units that with starting ages <= start of the Triassic and ending ages >= to the end of the Triassic. As always, show your code.

`>TrySubsetTriassic<- TriassicUnits[which(TriassicUnits[,"b_age"]<=252 & TriassicUnits[,"t_age"]>=201),]`

3) Repeat the above processes (download and subset) for the following geologic periods. The Cretaceous, Jurassic, Triassic (you don't have to download it twice), Permian, Carboniferous, Devonian, Silurian, and Ordovician. Show your code, but do not show me the downloaded data.

````R
>CretaceousUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Cretaceous&response=long&lith_class=sedimentary&format=csv")
>JurassicUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Jurassic&response=long&lith_class=sedimentary&format=csv")
>PermianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Permian&response=long&lith_class=sedimentary&format=csv")
>CarboniferousUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Carboniferous&response=long&lith_class=sedimentary&format=csv")
>DevonianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Devonian&response=long&lith_class=sedimentary&format=csv")
>SilurianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Silurian&response=long&lith_class=sedimentary&format=csv")
>OrdovicianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Ordovician&response=long&lith_class=sedimentary&format=csv")

> SubsetCretaceous<- CretaceousUnits[which(CretaceousUnits[,"b_age"]<=144 & CretaceousUnits[,"t_age"]>=66),]
> SubsetJurassic<- JurassicUnits[which(JurassicUnits[,"b_age"]<=200 & JurassicUnits[,"t_age"]>=145),]
> SubsetPermian<- PermianUnits[which(PermianUnits[,"b_age"]<=299 & PermianUnits[,"t_age"]>=252),]
> SubsetCarboniferous<- CarboniferousUnits[which(CarboniferousUnits[,"b_age"]<=359 & CarboniferousUnits[,"t_age"]>=299),]
> SubsetDevonian<- DevonianUnits[which(DevonianUnits[,"b_age"]<=419 & DevonianUnits[,"t_age"]>=359),]
> SubsetSilurian<- SilurianUnits[which(SilurianUnits[,"b_age"]<=443 & SilurianUnits[,"t_age"]>=416),]
> SubsetOrdovician<- OrdovicianUnits[which(OrdovicianUnits[,"b_age"]<=485 & OrdovicianUnits[,"t_age"]>=444),]
````

4) Make a vector named UnitFreqs that records the number of units present in each period. Show your code.

`> UnitFreqs<- c(nrow(SubsetCretaceous), nrow(SubsetJurassic), nrow(TrySubsetTriassic), nrow(SubsetPermian), nrow(SubsetCarboniferous), nrow(SubsetDevonian), nrow(SubsetSilurian), nrow(SubsetOrdovician))`

5) Find the mean and standard deviation of UnitFreqs not counting the Triassic. How many standard deviations above or below the mean is the number of Triassic Units? Show your code.

````R
> mean(UnitFreqs[-3])
[1] 2037.857
> sd(UnitFreqs[-3])
[1] 1322.319
````

The number of Triassic units is below one standard deviation of the mean since the number of records in the Triassic is 527.  

6) Given your answer to the above, do you believe that the Triassic has a statistically lower number of units than the other periods? Why?

All of the other periods are within one standard deviation of the mean with the exception of the Cretaceous period being slightly higher than one standard deviation above the mean. So I think the Triassic does have a statistically lower number of units than the other periods.

7) What if you consider both the Triassic and Jurassic as potential outliers? Explain (show your code) how you arrived at your answer.

````R
> UnitFreqs2<- c(nrow(SubsetCretaceous), nrow(SubsetPermian), nrow(SubsetCarboniferous), nrow(SubsetDevonian), nrow(SubsetSilurian), nrow(SubsetOrdovician))
> mean(UnitFreqs2)
[1] 2220.833
> sd(UnitFreqs2)
[1] 1347.96
````

The Triassic is still below one standard deviation of the mean so this is an outlier but the Jurassic value is within one standard deviation when considered an outlier and when it is not considered an outlier so only the Triassic is an outlier.

> generally we use more than 1 standard deviation for significance ~2, but this is fine.

## Problem Set 3

1) Download and plot a map of all North American geologic columns (no color). Show your code.

````R
> URL<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
> GotURL<-getURL(URL)
> AllMap<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
> plot(AllMap)
````

2) On top of your map from Question 1, plot a map of all North American columns with Induan-Anisian sedimentary units. Use the Olenekian hexcode color for this map. You can look up the Olenekian hexcode through the /defs/intervals route.

````R
>URL2<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1&lith_class=sedimentary&interval_name=Induan"
>URL3<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1&lith_class=sedimentary&interval_name=Anisian"
> GotURL2<-getURL(URL2)
> GotURL3<-getURL(URL3)
> IMap<-readOGR(GotURL2,"OGRGeoJSON",verbose=FALSE)
> AMap<-readOGR(GotURL3,"OGRGeoJSON",verbose=FALSE)
> plot(AllMap)
> plot(IMap, col="#A4469F", add=TRUE)
> plot(AMap, col="#BC75B7", add=TRUE)
````

3) Using the downloadPBDB( ) function from previous labs. Download all occurrences of animal fossils in the Paleobiology Database of Induan-Anisian age. Using the points( ) function, plot all of these occurrences on the map you made in question 2 as solid circles. If you do not remember how to use points, you can consult previous labs or use help(points). Show your code. Save this map for later questions.

````R
> DataPBDB<- downloadPBDB(Taxa=c(“Animalia”), StartInterval=”Induan”, StopInterval=”Anisian”)
> points(DataPBDB[,"lng"], DataPBDB[,"lat"], pch=19)
````

4) You can open a new plot window using quartz( ) if you are on a mac or `windows( ) if you are on a windows machine. Download and plot a map of all North American geologic columns (no color) - i.e., repeat Question 1 in this new plot window. On top of this map, plot a map of all North American columns with Lopingian aged sedimentary units. Use the appropriate Lopingian hexcode color for this new map. Show your code.
````R
> quartz(plot(AllMap))
> URL4<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1&lith_class=sedimentary&interval_name=Lopingian"
> GotURL4<-getURL(URL4)
> LMap<-readOGR(GotURL4,"OGRGeoJSON",verbose=FALSE)
> plot(LMap, col="#FBA794", add=TRUE)
````

5) Download all occurrences of animal fossils in the Paleobiology Database of Lopingian age. Plot all of these occurrences on the map you made in question 2 as solid circles. Show your code.
````R
> DataPBDB2<- downloadPBDB(Taxa=c("Animalia"), StartInterval="Lopingian", StopInterval="Lopingian")
> points(DataPBDB2[,"lng"], DataPBDB2[,"lat"], pch=19)
````

6) Compare and contrast your Induan-Anisian map versus your Lopingian map. 

There is a not a noticeable drop in sedimentary units in North America across the P/T boundary but there is a substantial drop in reported fossils.  Based on these maps, there seems to be an artifact of poor sampling that causes the reported drop in diversity since the amount of sedimentary packages doesn’t seem to decrease but the number of reported fossils is much lower.
