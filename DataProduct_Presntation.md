Pitch for Shiny App
========================================================
## Shiny app: Bloomington, IL house sale prices

author: Chris Reisinger 

date: 11/22/2015



Motivation
========================================================

I wanted to take a quick look in how the the sale price of a house is affected by different aspects of the house in my area.  Specifically, I wanted to see how the following house characteristics affected the sale price.

- Total Square Feet of the house
- The neighborhood in which the house is in
- The exterior type of the house (e.g. vinyl siding, wood siding, brich, etc.)
- Having a finished basement or not

Method
========================================================
I went to the Bloomingon Tax Assessor's website and had to manually copy house sale information from their website and save it into a CSV.

- Bloomington Tax Assessor's Website:
   http://www.wevaluebloomington.org/Start.asp

I only used housing sales from 2009-2015.

I only included residential sales

Code part 1
========================================================

```r
house<-read.csv("HouseValues.csv")
library(ggplot2);library(scales)
p<-ggplot(house,aes(TotalSF,SalePrice))
p<-p+scale_x_continuous(name="Total Square 
   Feet",labels=comma)+
   scale_y_continuous(name="Last Sale 
   Price",labels=dollar)+ggtitle("House 
   Sales")
p<-p+geom_point(aes(colour=factor(NH),
   size=factor(FinBsmt)),alpha=0.5)+
   scale_size_discrete(range = c(4,7))
```

Code part 2
===

```r
p<-p+geom_point(aes(shape=factor(Story)))+
   scale_shape_manual(values=1:12)+
   theme(legend.key=element_blank())
p<-p+guides(colour = guide_legend(nrow = 13,
   override.aes = list(size=5)))
```

Plot
========================================================

<img src="DataProduct_Presntation-figure/unnamed-chunk-3-1.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" width="1920px" />

Shiny App
========================================================
- There are over 5,000 properties included in this plot which makes it very difficult to read.  
- It would be handy to filter out some of the information to get a better sense of the data.
- That is why my shiny app located belew is such a great app.  You still have all the access to the data, but in a dynamic plot to dig into the information.
   https://careisin.shinyapps.io/DataProduct_Project
- In the shiny app, it is very obvious that certain neighborhoods have a higher sale price for other neighborhoods for houses with the same square footage.  It is also fairly obvious that houses with finished basements are higher on the plot than ones without finished basement.  
