---
title: COVID-19 Prison Data by NYT
author: Theo Hartsook
Date: 2021 June 15
---

### Note: This report shows summary information from New York Times' COVID-19 data available at this website: [https://github.com/nytimes/covid-19-data](https://github.com/nytimes/covid-19-data)

## 1. Load the prisons data in R

```r 
fac = read_csv('covid-19-data/prisons/facilities.csv')
```

```
```

## 2. Create a base map of the United States.
```r
library(maps)
library(mapdata)

usa = map_data('usa')
states = map_data('state')

usa_base = ggplot(data=states) +
	  geom_polygon(aes(x=long, y=lat, fill=I('white'), group=group), color='gray') +
	  coord_fixed(1.3) +
	  guides(fill=FALSE)
```

<center>
<img src='prison_loc.png' width=500> </img>
</center>

```r
usa_base +
	geom_point(data=fac %>% filter(facility_state=='Nevada'),
	aes(x=facility_lng, y=facility_lat, cex=latest_inmate_population), color='red', alpha=0.3) +
	coord_fixed(xlim=c(-130, -60), ylim=c(25,50), ratio=1.3)
```

<center>
<img src='nevada_prisons.png' width=500> </img>
</center>