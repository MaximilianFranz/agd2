# Analysetechniken für große Datenbestände 2

#Intro 
#Mathematik und Grundlagen
...
## Abstands- / Ähnlichkeitsmaße 
#### String-Matching Problem
> Problemstellung: Namenserkennung. # Wie ich dazu gekommen bin 
 - Ein Freund hat mich darauf verwiesen 
 - Master-Key System --> komischer Ansatz 
 - Danach viel ungeleitete Ansätze und nach __Thich Nath Hanh__
 - Später auch Calm und Headspace verwendet --> beide sehr gut! 
 - Fast tägliche Übung, die Klarheit und Gelassenheit bringt, zum Beispiel auch nach einem stressigen Tag, wenn gerade alles zu viel wird. 
 - Denn meditieren hilft mir zu Abstand herzustellen zwischen dem was passiert und wie es mir geht. 
 - Durch Meditation kann ich viel aufmerksamer als früher noch Gefühlsveränderungen wahrnehmen und so bspw. bewusst wahrnehmen, wenn ich traurig / überwältigt / überfordert werde und entsprechend eingreifen. Selbe Instanz kann in versch. Variantene dargestellt werden. (Abkürzung, Formatting, Spitznamen, ...)


##### <a name="edit"></a>Editierdistanz (Levenstein-Distanz mit DP)
   - Einfügen, Löschen und ersetzen eines Buchstaben
   - Normalisieren mit $d(x,y) / \max(l(x), l(y))$.

##### <a name="needle"></a> Needleman-Wunch-Maß
Als Verallgemeinerung der [Editierdistanz](#edit).
   - Verwendet Score-Matrix statt, *gleich teuere* Änderungen. (Bsp. e-a ist *ähnlicher* als d-f).

> Das Matching funktioniert nur ohne *Überkreuzungen*, damit DP funktioniert. 

##### <a name="penale"></a> Penale für affine Lücken 
Unterscheidung zwischen *öffnen* und *fortsetzten* von Lücken. so werden lange Lücken weniger stark penalisiert.

##### Smith-Waterman Maß 
Suche lokale Ausrichtung, statt global zu betrachten. 
__Bsp__:
```
„Prof. John R. Smith, Univ of Wisconsin“ 
„John R. Smith, Professor“
```

##### Jaro-Maß 
 - Betrachte alle gemeinsame Buchstaben in $y$ und $x$. 
 - Bilde Folge dieser gemeinsamen Buchstaben in jeweils $x$ und $y$. 
 - $c$ ist Anzahl übereinstimmender Buchstaben, $t$ ist Anzahl der Transpositionen.

##### Dynamic Time Warping
 - Entsprechung von Needleman-Wunch auf diskrete Zeitreihen. 

#### Hochdimensionale Räume
##### Mahalanobis-Distanz
 - Mithilfe einer Kovarianzmatrix $S$ normalisieren wir Distanz von Punkten zum Clustermittelpunkt.
 - $d(x,y) = \sqrt{(x-y)^T S^{-1}(x-y)}$

# Fundamentale Datenanalysetechniken (Wdh.)
## Datenreduktion für Klassifikation 
### Auswahl wichtiger Attribute 
#### <a name="infogain"></a> Information Gain 
> Anwendung: Training eines Entscheidungsbaumes. Welches Attribut wird nach welchen Werten gesplittet?

Betrachte den gewichteten Durchschnitt der Spaltenweisen (je Attributwert) Entropie um festzustellen, welche Attribute nützlich sind. 
 - Für diskrete Attribute 
 - Für kontinuierliche Attribute

##### Gain Ratio 
Normalisierung nach Anzahl der Splitbereiche. Dadurch soll Overfitting reduziert werden. 
> Bsp: Kreditkartennummer hat sehr hohen (perfekten) Information Gain, hat aber viele Attributwerte und daher geringe Gain Ratio.
 
#### <a name="gini"></a> _GINI_ Index

## Association Rules 
> Wiederholung der Grundlagen.

__Problem__: Manche Kennzahlen sind je nach Fall nicht aussagekräftig. (Siehe Beispiel (I), Videoverleih)

### Lift 

### $\Chi^2$-Wert 

### Vergleich versch. Maße 
![Screenshot 2019-05-16 at 08.17.42](/assets/Screenshot%202019-05-16%20at%2008.17.42.png)

Problem mit Lift: Werte für Lift sind unterschiedlich, auch wenn $D_1$ und $D_2$ in der Aussage bzgl. Milch und Kaffee eigentlich sehr ähnlich sind. Lift hängt aber von $\overline{mc}$ ab, also von der Menge der Transaktionen die weder Kaffee noch Milch enthalten. 

Lösung: Cosine Maß, dort wird $\overline{mc}$ gekürzt. (*Nachrechnen*!) Die Wurzel des Nenners gleicht die *Ungerechtigkeit* wieder aus. 

##### Null-Invarianz 
Maße, die nicht von Transaktionen abhängen, die keines der betrachteten Items enhalten heißen *Null-Invariant*. Lift ist **nicht** *null-invariant*. 


## Clustering 
### Problemstellung definieren
 - *k-means*: Clustermittelpunkte aus dem Datenbestand 
 - SSQ-Minimierung: Clustermittelpunkte müssen keine Datenpunkte sein. 
 - Facility Location: k ist nicht fixiert. Minimiere $FC(N,C) = z \cdot |C| + \sum_{i = 1}^{|C|} \sum_{x \in N_i} d(x,c_i)$. Der Name geht auf die platzierung von Lagern bspw. zurück, die sowohl die Distanz zum Lager als auch die Anzahl der Lager berücksichtigen muss. (Ggf. Fixkosten für jedes Lager).

 ### Alternate Clustering 
 __Problem__: Wenn das Clusteringergebnis nicht zufriedenstellend sind, will man ggf. Änderungen vornehmen. Neu generieren und zufällig ausprobieren ist ineffizient und intelektuell aufwändig.

 __Zielsetzung__: Finde Clustering, das möglichst neu ist. 

 __Lösung__: Betrachte beim agglomerativen Clustering sogenannten *should-not-link* constraints, die entweder gegeben sind oder aus den vorherigen clusterings erstellen werden. (e.g. Elemente des selben clusters sollen nicht nochmal zusammen in ein Cluster.) Betrachte dann den Quotienten $\frac{d(q_1, q_2)}{d(o_1,o_2)}$ des qualitativen und unähnlichen Paar-Abstands. 


 # Hochdimensionale Daten
 ## Similarity and Distance 
 > In hochdimensionalen Räumen funktionieren klassische Distanzmaße nicht richtig. 

 __Beispiel__: Euklidische Distanz: Mit höheren Dimensionen nimmt der Kontrast ab, d.h. Distanzen werden *ähnlicher*. Vgl. Theorem. 

 
## Instability 
Problem das bei NN-Distanzen auftreten kann. 

## Problems in Multi-Dimensional space 
### Expected NN-Distance 
*Def:* Gamma Function.

> How many datapoints $k$ are expected to lie within a sphere of radius $r$? 


### Distances grow similar
![Screenshot 2019-05-23 at 08.15.11](/assets/Screenshot%202019-05-23%20at%2008.15.11.png)
Erhöhte Dimension (x-Achse) führt zu weniger Kontrast zwischen den Clustern bzw. zwischen Clustern und Noise. Außerdeml rücken *min, max, mean* Distanz immer näher zusammen. 


### Most of the Space is empty
> Various illustrations of the correlation of dimension and *emptyness*.
#### Interesting geometric behaviour
The biggest sphere within a $d$-dimensional cube contains a fraction of the space: 

![Screenshot 2019-05-23 at 08.29.04](/assets/Screenshot%202019-05-23%20at%2008.29.04.png)

#### Bereichsanfragen funktionieren nicht
Ein Großteil der Minimum-Bounding-Box ist trotzdem leer und es entsteht eine große Menge *Verschnitt*. 

### Volume of Spherical Shell 
In high dimensional space a thin shell of the sphere contains almost all the volume. 

$$
\frac{V_{sphere}(r) - V_{sphere}(r(1-\epsilon))}{V_{sphere}(r)}
$$
goes towards $1$ for $d \to $ 

### Distributions show *strange* behaviour
![Screenshot 2019-05-23 at 08.37.19](/assets/Screenshot%202019-05-23%20at%2008.37.19.png)
Given the radius of the sphere around the mean $\mu$, how likely is a point within that sphere? 
Intuition is that most points are around the mean, but this doesn't count for high-dimensional space. 


### Tree-based indizes are useless
$l_{max} < E[\text{NN-dist}]$ for large d.
### Behaviour in high-dimensional space 
 1. The Shell is the sphere 
 2. Cube is most likely empty
 3. Distances grow similar 
 4. Expected NN-Distances grow 
 5. Distributions are strange
 6. Tree-based indizes are useless

# Clustering und Outlier detection 
## Projected Clustering
**optimal**: many objects in as many dimensions as possible (trade-off)
Because increasing dimension usually reduces the number of particular object-sets (clusters) (see problems with high-dim space)

### ProClus
 - See AgD I lecture

### Control clustering with $\alpha$ and $\beta$
 - $\alpha$: Size of the cluster as fraction of the dataset
 - $\beta$: When adding a dimension, at least fraction $\beta$ of the cluster remains intact.

 ### Projected Clustering via Cluster Cores (P3C)
 > explaining the essential bottom up approach over dimensions is sufficient. 

1. Look at 1-dim subspaces 
2. Find irregularities, intervals with many objects
3. Merge dimensions together until the decrease in 'cluster-objects' is too big. 
4. Outlier Detection using Mahalanobis distance and Chi-Square test
5. Detect further relevant attributes by considering dimensions that were deemed uniformly distributed initially. 
6. Refine signatures by shrinking intervals of the p-signatures to the minimum. 

#### Expectation Maximization
 - One datapoint can belong to many clusters 
 - Create Matrix of belonging () and run Expectation Maximization 

## Subspace Clustering
### HiCS [^1]
 1. Suche Teilräume mit 'hohem Kontrast' 
 Hoher Kontrast is definiert über die Wahrscheinlichkeitsverteilung (PDF) einer Dimension im Vergleich zur Joint PDF mehrerer Dimensionen. Weicht die Verteilung der Kombination stark von der Verteilung bei Annahme von Unabhängigkeit ab, so ist der Teilraum vermutlich *interessant*. 
 Generiere dazu die Conditional PDF, indem man kleine Streifen über einzelne Dimensionen legt. Wie groß sind diese Streifen? Definition nicht über breite, sondern Menge der Datenobjekte aus dem Datenbestand. 
 

 ### GMD 
 **Motivation**: Contrast alone leads to redudant results of dimension-subsets. 
 **Solution:** Iterating over each of the dimensions, order the remaining dimensions $j$ according to the contrast that the subspace would have if the fixed dimension is combined with $j$. 

 ### Object-basiertes Clustering. 
 


 [^1]: hics original paper http://data.bit.uni-bonn.de/publications/ICDE2012.pdf