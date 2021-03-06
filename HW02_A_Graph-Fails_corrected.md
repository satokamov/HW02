What went wrong?
================
Sherzod Tokamov

``` r
knitr::opts_chunk$set(echo = TRUE, error = TRUE)
```

## HW02 Part A

In this document, I will add some examples of some coding mistakes, it
is up to you to figure out why the graphs are messing up.

### First load packages

It is always best to load the packages you need at the top of a script.
It’s another common coding formatting standard (like using the
assignment operator instead of the equals sign). In this case, it helps
people realize what they need to install for the script and gives an
idea of what functions will be called.

It is also best coding practice to only call the packages you use, so if
you use a package but end up tossing the code you use for it, then make
sure to remove loading it in the first place. For example, I could use
`library("tidyverse")` but since this script will only be using ggplot2,
I only load ggplot2.

``` r
library(ggplot2)
```

    ## Warning in as.POSIXlt.POSIXct(Sys.time()): unknown timezone 'zone/tz/2020a.1.0/
    ## zoneinfo/America/Chicago'

``` r
library(magrittr) #so I can do some piping
```

### Graph Fail 1

What error is being thrown? How do you correct it? (hint, the error
message tells you)

``` r
data(mpg) #this is a dataset from the ggplot2 package

mpg %>% 
  ggplot(mapping = aes(x = cty, y = hwy, color = "blue")) %>% + #change "city" to "cty"
  geom_point()
```

![](HW02_A_Graph-Fails_corrected_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

### Graph Fail 2

Why aren’t the points blue? It is making me blue that the points in the
graph aren’t blue :\`(

``` r
ggplot(mpg, aes(x = displ, y = hwy)) + #move aes to ggplot, specify color in geom.
  geom_point(color = "blue")
```

![](HW02_A_Graph-Fails_corrected_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

### Graph Fail 3

Two mistakes in this graph. First, I wanted to make the the points
slightly bolder, but changing the alpha to 2 does nothing. What does
alpha do and what does setting it to 2 do? What could be done instead if
I want the points slightly bigger?

Second, I wanted to move the legend on top of the graph since there
aren’t any points there, putting it at approximately the point/ordered
pair (5, 40). How do you actually do this? Also, how do you remove the
legend title (“class”)? Finally, how would you remove the plot legend
completely?

``` r
mpg %>% 
ggplot() + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class), size = 2) + #change alpha = 2 to size =2. alpha sepecifies opacity and needs to be 0 - 1.
  theme(legend.direction = "horizontal") + 
  theme(legend.position = c(0.6, 0.9)) + #values 0-1, in proportion to the graph, where 0, 0 is the left bottom of the graph
  theme(legend.title = element_blank()) #removes legend
```

![](HW02_A_Graph-Fails_corrected_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

### Graph Fail 4

I wanted just one smoothing line. Just one line, to show the general
relationship here. But that’s not happening. Instead I’m getting 3
lines, why and fix it please?

``` r
mpg %>% 
ggplot(mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = drv)) + #specifyin color in ggplot will apply colors to everything (i.e. points, lines, etc). So moving color = drv to geom_point will only apply color to the points, and geom_smooth will now fit a line to the entire plot, not individual colored points. 
  geom_smooth(se = F) #se = F makes it so it won't show the error in the line of fit
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](HW02_A_Graph-Fails_corrected_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Graph Fail 5

I got tired of the points, so I went to boxplots instead. However, I
wanted the boxes to be all one color, but setting the color aesthetic
just changed the outline? How can I make the box one color, not just the
outline?

Also, the x-axis labels were overlaping, so I rotated them. But now they
overlap the bottom of the graph. How can I fix this so axis labels
aren’t on the graph?

``` r
ggplot(data = mpg, mapping = aes(x = manufacturer, y = cty)) + 
  geom_boxplot(fill = "red") + #this will create a boxplot with all boxes red
  theme(axis.text.x = element_text(angle = 45, vjust = 0.5)) #vjust allows to move the x-axis labels.
```

![](HW02_A_Graph-Fails_corrected_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->
