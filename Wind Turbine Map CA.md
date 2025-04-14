install.packages("ggplot2")
install.packages("dplyr")
install.packages("mapdata")
library(ggplot2)
library(dplyr)
library(mapdata)
##Step A create dataframe
states <- map_data("state")
california <- states %>% filter(region == "california")
head(california)

##Step B Load data
load('C:/Users/Luckh/OneDrive/Documents/School/DSC/DATA/wind_turbines.rda')
ls()
head(wind_turbines)
wind_ca <- wind_turbines %>%
  filter(t_state == "CA")
head(wind_ca)

###Step C use GGplot to visualize California
ggplot(data = california, aes(x = long, y = lat, group = group)) +
  geom_polygon(fill = "lightgray", color = "black") +
  coord_fixed(1.3) + 
  theme_minimal() +
  labs(title = "Map of California")

##Step D Wind Turbine Plot Locations in CA
names(wind_ca)
ggplot(data = california, aes(x = long, y = lat,)) +
  geom_polygon(fill = "lightgray", color = "black") +
  geom_point(data = wind_ca, aes(x = xlong, y = ylat), color = "red", size = 1) +
  coord_fixed(1.3) +
  guides(fill = "none") +
  theme_minimal() +
  labs(title = "Wind Turbine Locations in California")
head(wind_ca)


