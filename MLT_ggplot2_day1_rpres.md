ggplot2
========================================================
author: Malie Lessard-Therrien and Etienne Low-Décarie 
date: May 8, 2017
width: 1920
height: 1080


What is a graph?
===

- Statistics and design combined
- Explore and explain
- Communicating results


ggplot2
===

Beautiful and flexible

![Pretty ggplots](./ggplot2_pres-figure/pretty_examples.png)



Outline (ggplot2)
===

Day I

Your first ggplot plot
- Basic scatter plot 
- Exercise 1

Grammar of graphics
- More advanced plots
- Aesthetics, Geometrics
- Exercise 2

Facets
- Exercise 3

Saving your graphs

***    

Day II

Pretty graphs for presentation
- Fine tunning
- Package cowplot
- Exercise 4

Maps
    


Install/load ggplot2
===


```r
if(!require(ggplot2)){install.packages("ggplot2")}
require(ggplot2)
```


Iris dataset
===

- Edgar Anderson
- RA Fischer

![Iris flowers](./ggplot2_pres-figure/iris_flowers.png)



```r
head (iris)
```

```
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
4          4.6         3.1          1.5         0.2  setosa
5          5.0         3.6          1.4         0.2  setosa
6          5.4         3.9          1.7         0.4  setosa
```


What to use when
===

Explore your data using function "qplot"
- For you and your colleagues
- Quick
- Default settings can't be changed
- like the function "plot" in R-base


Explain a pattern (or lack of) in your data using function "ggplot"
- For presentation or publication
- All settings must be specified
- Flexible (you have the control over all settings)


Your first graph with ggplot2 
===

A basic scatter plot

```r
qplot(data=iris,
      x=Sepal.Length,
      y=Sepal.Width)
```

***

![plot of chunk unnamed-chunk-5](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-5-1.png)


Change axis names 
===


```r
qplot(data=iris,
      x=Sepal.Length,
      y=Sepal.Width,
      xlab="Sepal length (mm)",
      ylab="Sepal width (mm)")
```

![plot of chunk unnamed-chunk-6](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-6-1.png)

Exercice 1
===
produce a basic plot with built in data

```
data()
CO2
?CO2

```
WARNING: THERE ARE MULTIPLE CO2/co2 datasets
(CASE SENSITIVE, use capitals)


Grammar of graphics (gg)
===

2 principles:
- distinc layers of graphical elements
- meaningful plots using aesthetic mapping

***

![layers of a plot](./ggplot2_pres-figure/separate_elements.png)


Graph elements
===

3 essentials:
- Data (what you collected, in the right format)
- Aesthetics (aes)
- Geometries (geom)


4 optionals:
- Facets
- Coordinates
- Themes
- Statistics


***


![layers of a plot](./ggplot2_pres-figure/graph_layers.png)



Aesthetics
===

set with the aes() function
- color ("outside" color)
- fill ("inside" color)
- shape (of points)
- linetype
- size (of points or line)
- position (i.e., on the x and y axes)
- group (that a point belongs to)
- alpha (transparency of the point)


Geometic Objects 
===

set with the "geom_..." command

Ex:
- points (geom_point, for scatter plots, dot plots, etc)
- lines (geom_line, for time series, trend lines, etc)
- boxplot (geom_boxplot, for, well, boxplots!)
- violins (geom_violin, region inside the violin contains all of the observed data)

A plot must have at least one geom; there is no upper limit. You can add a geom to a plot using the + operator


Available elements
===

http://ggplot2.tidyverse.org/reference/

<iframe src="http://ggplot2.tidyverse.org/reference/" width="1000" height="800">
  <p>Your browser does not support iframes.</p>
</iframe>



How it works
===

- 1. create a simple plot object

```r
plot.object<-qplot() # to explore 
or
plot.object<-ggplot() # to explain 
```
- 2. add graphical layers/complexity

```r
plot.object<-plot.object+layer()
```
- 3. repeat step 2 until satisfied  
- 4. print your object to screen (or to graphical device)  

```r
print(plot.object)
```


Scatter plot as an R object with qplot
===


```r
basic_graph<-qplot(data=iris,
                  x=Sepal.Length,
                  y=Sepal.Width,
                  xlab="Sepal length (mm)",
                  ylab="Sepal width (mm)")

print(basic_graph)
```

![plot of chunk unnamed-chunk-11](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-11-1.png)


Scatter plot as an R object with ggplot
===
Note: aes() and geom_point()


```r
basic_graph <- ggplot(data=iris,
                    aes(x=Sepal.Length,
                        y=Sepal.Width))+
                      xlab("Sepal length (mm)")+
                      ylab("Sepal width (mm)")+
                      geom_point()
                    
print (basic_graph)
```

![plot of chunk unnamed-chunk-12](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-12-1.png)

Geometric example
===
Scatter plot with colour and shape


```r
basic_graph <- basic_graph+
              aes(colour=Species,
                  shape=Species)

print(basic_graph)
```

![plot of chunk unnamed-chunk-13](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-13-1.png)


Geometric example
===
Scatter plot with linear regression

Add a geom (eg. linear smooth)


```r
basic_graph_lm <- basic_graph+
  geom_smooth(method="lm", se=F)

print(basic_graph_lm)
```

![plot of chunk unnamed-chunk-14](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-14-1.png)

Exercise 2
===

Produce a colorful plot containing linear regressions with built in data

```
CO2
?CO2
data()
```
WARNING: THERE ARE MULTIPLE CO2/co2 datasets
(CASE SENSITIVE, use capitals)

<div class="centered">

<script src="countdown.js" type="text/javascript"></script>
<script type="application/javascript">
var myCountdown2 = new Countdown({
    							time: 300, 
									width:150, 
									height:80, 
									rangeHi:"minute"	// <- no comma on last item!
									});

</script>

</div>


Geometric example  
===

Categorical x-axis


```r
basic_graph_cat <- ggplot(data=iris,
                          aes(x=Species,
                              y=Sepal.Width))+
                              xlab("Species")+
                              ylab("Sepal width (mm)")+
  geom_point()
  
print (basic_graph_cat)
```
.  
.  
.  

```r
basic_graph_cat_bx <- basic_graph_cat+
  geom_boxplot ()

print (basic_graph_cat_bx)
```
***
![plot of chunk unnamed-chunk-17](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-17-1.png)

![plot of chunk unnamed-chunk-18](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-18-1.png)


Geometric example  
===

Categorical x-axis, geom_violin

![Violin fruit type](./ggplot2_pres-figure/Violin_FFD_ft.jpeg)


Facets
===

Divide the data graphically

facet_grid(rows~columns)


```r
iris_facets <- basic_graph + 
              facet_grid(. ~ Species)

print (iris_facets)
```
***
![plot of chunk unnamed-chunk-20](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-20-1.png)

Exercise 3
===

Create a colorful graph with the data you have used using geoms and facets


```
CO2
?CO2
data()
```
<div class="centered">

<script src="countdown.js" type="text/javascript"></script>
<script type="application/javascript">
var myCountdown3 = new Countdown({
    							time: 300, 
									width:150, 
									height:80, 
									rangeHi:"minute"	// <- no comma on last item!
									});

</script>

</div>


Facets
===

Using CO2 data

```r
head (CO2)
```

```
  Plant   Type  Treatment conc uptake
1   Qn1 Quebec nonchilled   95   16.0
2   Qn1 Quebec nonchilled  175   30.4
3   Qn1 Quebec nonchilled  250   34.8
4   Qn1 Quebec nonchilled  350   37.2
5   Qn1 Quebec nonchilled  500   35.3
6   Qn1 Quebec nonchilled  675   39.2
```

Facets
===


```r
CO2_graph_facets<-ggplot(data=CO2,
                aes(x=conc,
                    y=uptake,
                    colour=Treatment))+
  geom_point()+
  facet_grid(.~Type)
  
print(CO2_graph_facets)
```

![plot of chunk unnamed-chunk-22](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-22-1.png)

Groups
===

Problems when adding the geom_line


```r
print(CO2_graph_facets+geom_line())
```

![plot of chunk unnamed-chunk-23](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-23-1.png)

Groups
===

Solution: specify groups


```r
CO2_graph_fg<-CO2_graph_facets+geom_line(aes(group=Plant))

print(CO2_graph_fg)
```

![plot of chunk unnamed-chunk-24](MLT_ggplot2_day1_rpres-figure/unnamed-chunk-24-1.png)

Help
===

- R-help
- R Cookbook (ex facets: http://www.cookbook-r.com/Graphs/Facets_(ggplot2)/
- Cheatsheets (see https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)
- Stackoverflow (google your question with ggplot2)

Saving plots
===


```r
pdf("./Plots/todays_plots.pdf")
  print(basic_graph)
  print(basic_graph_lm)
  print(basic_graph_cat_bx)
  print(iris_facets)
  print(CO2_graph_facets)
graphics.off()
```

all other R-base save functions available:  
`bmp()`, `jpeg()`, etc

Saving plots
===

ggsave: saves last plot and guesses format from file name


```r
ggsave("./Plots/todays_plots.jpeg", iris_facets)
```
