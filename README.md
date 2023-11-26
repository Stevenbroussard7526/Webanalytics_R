# Preparation: Load packages and the dataset used for this assignment.
webAnalytics= read.csv("WebAnalytics4.csv")
library(ggplot2)



#Q1:
# Use base R to draw the scatterplot of TimeOnPage (x axis) versus PageViews (y axis).
# Make sure to change the shape, color, and size of the points. 
# Also, set your own labels for both axes and add a title to the plot. 
# In addition, set a limit on the x axis to be between 0 and 300,000.

plot(PageViews~TimeOnPage,webAnalytics, type="p",
     pch=18,col="purple",cex=1,
     xlab="Time on Page",
     ylab="Page Views", 
     xlim=c(0,300000),
     main="How Much Time Page Visitors Spend on Web Page")


#Q2:
# Recreate the same plot using ggplot. 
# (You can refer to ggplot cheatsheet or its reference page online for an overview of all the arguments.)
# (For example, here are some examples of geom_point() options: 
# https://ggplot2.tidyverse.org/reference/geom_point.html

options(scipen=999)
ggplot(webAnalytics,aes(TimeOnPage,PageViews, xmin=0, xmax=300000)) +
  geom_point(shape=18,color="purple",size=1.5,alpha=.25) +
  labs(x="Time on Page",
       y="Page Views",
       title="How Much Time Page Visitors Spend on Web Page")
  

#Q3:
# a. Use ggplot to draw the scatterplot of TotalDownloads (x axis) versus ConversionRate (y axis).
# b. Draw a similar plot but add jitters. Use a theme and a color.
# (For both parts, read TotalDownloads as a factor for visual clarity on the x axis.)

#A
ggplot(webAnalytics,aes(factor(TotalDownloads),ConversionRate)) +
  geom_point(shape=18,size=3,alpha=.2) +
  labs(x="Total Downloads",
       y="Conversion Rate")

#B
ggplot(webAnalytics,aes(factor(TotalDownloads),ConversionRate)) +
  labs(x="Total Downloads",
       y="Conversion Rate",
       title="Total Downloads vs. Conversion Rate") +
  geom_jitter(alpha=.2,shape=18,color="red",size=3) +
  theme_bw()


#Q4:
# Create a boxplot with Region as categories (x-axis) and ConversionRate as the outcome of interest (y-axis).
# Change the (border/points) color of the boxplots.
# In addition, add a title, a subtitle, and a blank x axis label. 
# In so doing, adjust the location, size, and the color of the title and the subtitle.

ggplot(webAnalytics,aes(Region,ConversionRate)) +
  geom_boxplot(col="grey30",alpha=.2) + 
  labs(x="",title="Box Plot of Conversion Rate in Each Region",subtitle = "(Broken down by Region)")+
  facet_wrap(~Region,scales = "free_x")+
  theme(plot.title = element_text(hjust = 0.5,
                                  size = 20,
                                  color = "blue"),
        plot.subtitle = element_text(hjust=.5,
                                     size = 15,
                                     color="red"),
        panel.spacing.x = unit(15,units="mm")) +
  theme(legend.position = "none")


#Q5:
# Create the same box plot of Q4 but use facet wrap to separate by Source.
# Also, fill each boxplot with different colors based on Source and 
# add a color legend to the bottom of the plot

ggplot(webAnalytics,aes(Region,ConversionRate, fill=Source)) +
  geom_boxplot(col="grey30",alpha=.2) + 
  labs(x="",title="Box Plot of Conversion Rate in Each Region",subtitle = "(Broken down by Source)")+
  facet_wrap(~Source,scales = "free_x")+
  scale_fill_manual(values=c("purple",
                             "green",
                             "yellow",
                             "red"))+
  theme(plot.title = element_text(hjust = 0.5,
                                  size = 20,
                                  color = "blue"),
        plot.subtitle = element_text(hjust=.5,
                                     size=14,
                                     color = "red"),
        panel.spacing.x = unit(15,units="mm")) +
  theme(legend.position = "bottom")
