## Part I Questions

> Sorry, I graded it wrong the first time. Your final grade is 17.5/20


1) Your identifications (how many species do you recognize in the group, and which specimens belong to which species). Explain how and why you came to this conclusion.

+ Species A, 6 specimens: involute, under 28 diameter: Ammonites 2, 5, 6, 14, 23, 24
+ Species B, 2 specimens: evolute, under 28 diameter: Ammonites 12, 18
+ Species C, 4 specimens: involute, display growth lines, above 28 diameter: Ammonites 10, 16, 22, 25
+ Species D, 5 specimens: evolute, no growth lines, above 28 diameter: Ammonites 7, 11, 13, 15, 17
+ Species E, 8 specimens: involute, no growth lines, above 28 diameter: Ammonites 1, 3, 4, 8, 9, 19, 20, 21

2) The morphological features you used to distinguish each species, including whatever combination of qualitative or quantitative traits you think are important.

+ Diameter of shell, singling out notable smaller shells
+ Involute: outer whorl covers part of preceding whorls
+ Evolute: outer whorl does not cover part of preceding whorls
+ Growth lines present
  
3) The nature of ontogenetic change, if any, in the species. Explain your reasoning.

Only size changes, with the exception of the very small ammonites (species A and B) that have enough ribbing to appear mature

4) The possibility of sexual dimorphism as a cause of morphological differences and how you evaluated that possibility.

Since it is believed that some male ammonites are smaller and wider than females, I did not take small differences in size into account. There was no large variation in W/D values.


## Part II Questions - Subsection 1

1) Each element of the plethodon list has a name. What are they?

> Next time show what code you used to find the names.

2) Land, links, species, site, outline

3) What class is each object?

> I meant each object in the plethodon list, but I guess that wasn't clear. -0.25 points

Plethodon and hummingbirds are lists. <strike>Each element in plethodon is a character</strike>

4) Whare are the dimensions of the first object in the plethodon list?

<strike>13</strike>
> use dim(plethodon[[1]]) to find out.


## Part II Questions - Subsection 2

1) Use the hummingbird dataset. Which object in the list records the landmark data?

> You forgot to answer this? -1 point

2) Perform a procrustes on the landmark data. 

````R
ProcrustesHummingbirds<-gpagen(plethodon[["land"]])
````

> Why did you use the plethodon dataset and not hummingbirds? - 0.25 points

3) Perform a PCA on the hummingbird data.

````R
plotTangentSpace(ProcrustesHummingbirds[["coords"]],warpgrids=FALSE,verbose=FALSE)
````

4) How many "species" of hummingbird are there?

<strike>3. I’m not sure I was getting the correct plot to show up this time</strike>

> You didn't, presumably because you performed the anaysis on the plethodon dataset instead of hummingbirds, see your answer to question 2. -1 points

## Part III Questions

1) What is the synapomorphy of the clade containing species D and E?

Fangs longer than 6 inches

2) What is a plesiomorphic character of that clade?

Sulfurous ordor

3) What is the synapomorphy of the clade containing species A and B?

Adorable eyelashes

4) Which taxa have a sulfurous odor?

C, D and E

5) What character distinguishes species D from species E?

Laser Death Ray

6) Are adorable eyelashes a synapomorphy or an autapomorphy?

<strike>autapomorphy</strike>

> Syanpomorphy, -0.25 points

7) Traditionally, the five taxa are grouped into three families. Determine if each family is monophyletic, paraphyletic, or polyphyletic.

+ Family 1: monophyletic
+ Family 2: polyphyletic
+ Family 3: monophyletic

8) More recently, species A has been grouped in a family with species D and E. Is this advisable? Why or why not?

No, species A has a more common ancestor with both B and C

9) Determine if the following groups are monophyletic, paraphyletic, or polyphyletic.

> - 0.25 points

+ Group 1: paraphyletic
+ <strike>Group 2: monophyletic</strike> polyphyletic
+ Group 3: paraphyletic
+ Group 4: monophyletic
+ Group 5: polyphyletic

## Part IV Questions
1) Assuming that *Gryphaea arcuata* represents the ancestor, what type of heterochrony is most likely responsible for evolution of these two species?

Paedomorphosis - *Gryphea gigantea*
Peramorphosis - *Gryphea mccullochi*

2) Which species of Gryphaea has undergone a greater degree of heterochrony?

Gryphaea gigantean – greater resemblance to juvenile traits

3) What type of heterochrony is represented in the Ollenus example??

Paedomorphosis 

