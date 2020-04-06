

### COVID19 India data

The data is compiled manually using the daily updates about the outbreak on Ministry of Health and Family Welfare site: https://www.mohfw.gov.in/

Will try to keep it as updated as possible. Please feel free point out any mistakes. 


### How to read the data in R

``` R
library(readr)
d <- read_csv("https://raw.githubusercontent.com/rahulnyk/COVID19_IndiaData/master/covid_19_india.csv")
```