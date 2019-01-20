---
layout: post
title: Transit Use 2018
date: 2019-01-19
type: post
tags: R

---

Tracking all the times I used transit continued in 2018. A tradition since 2014. This does not include my transit use on non-TTC systems. I took 234 rides in 2018. The only time I used tokens this year was to attend meetings at the airport.

Two-hour transfers were introduced partway through the year so I've counted a "ride" whenever I would be charged if I tapped my Presto card or deposited a token before two-hour transfers. 

|Media             |Total Rides|Total Cost ($)|
|:------------|---:|----:|
|Day Pass (shared) |   4|   0.00|
|Free			   |   2|   0.00|
|Presto			   | 226| 626.00|
|Token			   |   2|	6.00|


My rides were paid for using: Day Passes (4), Tokens (2), Presto (226), and other (2).

![Rides by Day of Week]({{ site.url }}/images/2019-01-19_transit_use/day of week-1.png)<!-- -->

Highest TTC use was on Sundays when I was going to axe throwing league for most of the year. I walk to/from work every day when I'm at my regular office so do not use the TTC most weekdays. Total rides each month show when I branched out for walks further away.

```r
monthly17 <- data17 %>% 
  group_by(month) %>%
  summarize(TotRides = sum(rides),
		TotCost = round(sum(cost),2))

p <- ggplot(monthly17, aes(month, TotRides)) + 
  geom_bar(stat = "identity") +
  scale_x_date(date_breaks = "1 month", 
               date_labels = "%b") +
  labs(title = "Rides By Month 2017",
  	x = "Month", y ="Total Rides")
```

![Rides by Month]({{ site.url }}/images/2019-01-19_transit_use/monthly plot-1.png)<!-- -->

## Year over year
Splitting day of week usage out by month for the past five years highlights the low weekday pattern in my transit use, except for 2017 when I was seconded to the airport for the summer. Higher Sunday use in 2018 for the first 8 months of the year is visible.

![Year-over-year Rides by Day of Week and Month]({{ site.url }}/images/2019-01-19_transit_use/year-over-year-1.png)<!-- -->

```r
annual_summary <- data_tot %>%
  group_by(as.factor(years)) %>%
  summarize(Cost = round(sum(cost),2), 
            Rides = sum(rides), 
            Cost_Per_Ride = round(Cost / Rides, 2),
            Work_Rides = sum((str_count(note, "GTAA"))* rides))
names(annual_summary)[1] = "Year"

```


|Year| Cost ($)| Rides| Cost/Ride|	Work Rides|
|----|-----:|----:|----:|----:|
|2014|	380.00|   206|	1.84|	3|
|2015|	369.00|   175|	2.11|  	3|
|2016|	350.00|  161|	2.17| 	2|
|2017|	696.00|   261|	2.67| 100|
|2018|	628.00|   234|	2.69|  31|


With Presto being the default for basically all my riding, the average cost of my rides is going up. I used the TTC for more personal riding than I have since 2014. I continue to have meetings at the airport so my work riding is still higher than it used to be before 2017.
