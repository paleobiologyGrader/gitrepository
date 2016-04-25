> 20/20

## Problem Set 1

1) Is North America currently (i.e., in the present) to the West or East of its position in the Cretaceous?

a. west

2) Look at the following line of code that you used before.

````R
plot(ModernMap,col=rgb(1,0,0,0.33),lty=0,add=TRUE)
````

Describe what this code is doing. A good answer will describe what each of the `plot( )` function arguments is doing - i.e., what is the meaning of col=, lty= and add=. As well, what does the `rgb( )` function do? What does it mean? Use google or the R `help( )` function.

Plot – plots given map, in this case ModernMap
Col – column indexes in ModernMap
Rgb(1,0,0,0.33) – refers to red, green and blue primaries, gives intensities of each color; 0.33 is transparency 
Lty – line type, in this case make the borders very thin

3) Download a map of the middle Cretaceous (Albian Epochs ~110 mys ago). Name it AlbianMap.

````R
AlbianMap<-downloadPaleogeography(Age=110)
````

4) Add `AlbianMap` to the plot you made earlier. The added continents should be colored green, and use the same level of opacity (translucence) as your CretaceousMap and ModernMap. Show your code!

````R
plot(AlbianMap,col=rgb(0,1,0,0.33),lty=0.01,add=TRUE)
````

5) Has there been more movement north and south or east and west in the Eastern Hemisphere since the Albian?

North/South

6) Has there been more movement north and south or east and west in the Western hemisphere since the Albian?

East/West

## Problem Set 2
1) Download and plot a new map of the Paleocene/Eocene boundary (Use google to find the age of this boundary, remember the downloadMap( ) function only takes whole numbers). You may use any color and level of opacity. Show your code.

````R
PEMap<-downloadPaleogeography(Age=56)
plot(PEMap,col=rgb(0,1,1,0.33),lty=0.01)
````

2) Download a dataset of Anthozoa occurrences from the paleobiology database ranging from the Paleocene through Eocene. Consult with previous labs if you do not remember how to do this. Show your code.

````R
> DataPBDB<-downloadPBDB(Taxa=c("Anthozoa"),StartInterval="Paleocene",StopInterval="Eocene")
````

3) How many occurences did you download?

````R
> dim(DataPBDB)
   [1] 2847   26
````

4) What are the names of columns of the PBDB data matrix you just downloaded. What does each column mean? If you do not know, consult with the API documentation.

````R
> names(DataPBDB)

"occurrence_no” : number of occurences
"record_type” : type of object
"reid_no: : If this occurrence was reidentified, a unique identifier for the reidentification. This value is a key for the reidentification table, and is probably useful only for debugging purposes. It does, at least, indicate that this was not the original identification of the occurrence.
"flags" : This field will be empty for most records. A record representing an identification that has been superceded by a more recent identification will have the letter R in this field.           
"collection_no"   The identifier of the collection with which this occurrence is associated.
"identified_name" : The taxonomic name by which this occurrence was identified. This field will be omitted for responses in the compact voabulary if it is identical to the value of accepted_name.
"identified_rank" : The taxonomic rank of the identified name, if this can be determined. This field will be omitted for responses in the compact voabulary if it is identical to the value of accepted_rank.
"identified_no" : The unique identifier of the identified taxonomic name. If this is empty, then the name was never entered into the taxonomic hierarchy stored in this database and we have no further information about the classification of this occurrence. In some cases, the genus has been entered into the taxonomic hierarchy but not the species. This field will be omitted for responses in the compact voabulary if it is identical to the value ofaccepted_no.  
"difference" : If the identified name is different from the accepted name, this field gives the reason why. This field will be present if, for example, the identified name is a junior synonym or nomen dubium, or if the species has been recombined, or if the identification is misspelled.     
"accepted_name" : The value of this field will be the accepted taxonomic name corresponding to the identified name. 
"accepted_rank" : The taxonomic rank of the accepted name. This may be different from the identified rank if the identified name is a nomen dubium or otherwise invalid, or if the identified name has not been fully entered into the taxonomic hierarchy of this databas. "accepted_no" : The unique identifier of the accepted taxonomic name in this database.    
"early_interval" : The specific geologic time range associated with this occurrence (not necessarily a standard interval), or the interval that begins the range iflate_interval is also given 
"late_interval" : The interval that ends the specific geologic time range associated with this occurrence, if different from the value of early_interval   
"max_ma" : The early bound of the geologic time range associated with this occurrence (in Ma)         
"min_ma" : The late bound of the geologic time range associated with this occurrence (in Ma)         
"reference_no" : The identifier of the reference from which this data was entered    
"paleomodel" : The primary model specified by the parameter pgm. This field will only be included if more than one model is indicated. "paleolng" : The paleolongitude of the collection, evaluated according to the primary model indicated by the parameter pgm.        
"paleolat" : The paleolatitude of the collection, evaluated according to the primary model indicated by the parameter pgm.       
"geoplate" : The identifier of the geological plate on which the collection lies, evaluated according to the primary model indicated by the parameter pgm. This might be either a number or a string.       
"phylum" :  The name of the phylum in which this occurrence is classified.       
"class" :  The name of the class in which this occurrence is classified.        
"order" : The name of the order in which this occurrence is classified.         
"family" : The name of the family in which this occurrence is classified.        
"genus" : The name of the genus in which this occurrence is classified. If the block subgenus is specified, this will include the subgenus name if any.         
````

5) Use the `points( )` function to plot each occurrence on the map you made previously (make sure to use the paleolatitude and paleolongitude coordinates). Show your code. If you do not know how to use the `points( )` function, consult the help file or use Google.

````R
> points(x=DataPBDB[,"paleolng"],y=DataPBDB[,"paleolat"])
````

6) Where are most of the Anthozoa occurrences in the Eastern Hemisphere (i.e., what region of the world)? Are Anthozoa primarily marine or freshwater organisms? What can you infer must have existed in this region of the world during this time?

Mid-Europe, along coast lines in all other regions. They are primarily marine organisms. There must have been an ocean covering most of Europe during the Paleocene/Eocene boundary. 

## Problem Set 3
1) Download a dataset of Perissodactyla occurrences from the PBDB that span the Paleogene. Show your code.

````R
> DataPBDB<-downloadPBDB(Taxa=c("Perissodactyla"),StartInterval="Paleogene",StopInterval="Paleogene")
````

2) What is the defining attribute of Perissodactyla? What are some prominent examples (e.g., lions, tigers, bears, oh my!)? [Hint: Neither lions, nor tigers, nor bears are members of Perissodactyla.]

Odd-toed Ungulates – mammals with an odd number of toes, ie zebras, horses, rhinos

3) Find collection number 112723 in the dataset you just downloaded in Question 1. Show your code.

````R
> thing<-subset(DataPBDB,DataPBDB[,"collection_no"]==112723)
````

> Always try to use meaningful variable names

4) What "geoplate" id (tectonic plate) is associated with this collection? What modern day region of the world does this geoplate id correspond to? The remaining questions will refer to this geoplate/region as region-X.

Indian Plate

````R
> thing[,"geoplate"]
[1] 501 501
> thing<-subset(DataPBDB,DataPBDB[,"geoplate"]==501)
> plot(PEMap,col=rgb(1,0,0,0.33),lty=0.01)
> points(x=thing[,"paleolng"],y=thing[,"paleolat"])
````

5) Subset your dataset of Perissodactyla occurrences to only include occurrences that occur in region-X. How many occurrences are there? Show your code.
84

````R
> dim(thing)
[1] 84 26
````

6) Using the maps we have created previously, making your own new maps, or using the Paleobiology Database Navigator tool, what is the general history of region-X from the Albian through to the present day?

Region-X moves from the middle of the Southern Hemisphere to the north and eventually collides with the Eurasian Plate, creating the Himalayas.  

7) There are also many Paleogene occurrences of Perissodactyla in present day China. Using the maps we have created previously, making your own new maps, or using the Paleobiology Navigator tool, evaluate the plausibility of each of the following scenarios? Thoroughly explain your reasoning and how you tested your ideas.

+ Species of Perissodactyla migrated from region-X to China during the Paleogene?

This is not likely, due to the massive ocean between region-x and China.  But, because there is no way to be 100% sure that our information is correct. There is a possibility that region-x and China were connected, and therefore it is possible that species of perissodactyla migrated from region-X to China. 

+ Species of Perissodactyla migrated from China to region-X during the Paleogene?

This is not likely, due to the massive ocean between China and region-x.  But, because there is no way to be 100% sure that our information is correct. There is a possibility that China and region-x were connected, and therefore it is possible that species of perissodactyla migrated from China to region-X. 

+ The species of Perissodactyla in China and region-X are unrelated and probably both came from a third region?
 
 It is possible that a distant ancestor originated from a third region, and migrated across both Eurasia and India when India was still connected to Africa (during the Jurassic). These animals would probably not preserved in the fossil record. Although this scenario is possible, I think it is the most unlikely. 
