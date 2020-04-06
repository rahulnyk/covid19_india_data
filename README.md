

### COVID19 India data

The data is compiled manually using the daily updates about the outbreak on Ministry of Health and Family Welfare site: https://www.mohfw.gov.in/

Will try to keep it as updated as possible. Please feel free point out any mistakes. 


The data is in the wide fromat with respect to the status (Recovered, Hospitalized or Deceased)

Whenever there is new data published, it is appended to the old csv, which means there may be several rows per state per day. 
Choose the max of the number of cases to avoid duplication. Here is an example

### How to read the data in R


``` R

  library(readr)
  data <- read_csv("https://raw.githubusercontent.com/rahulnyk/covid19_india_data/master/covid_19_india.csv") %>%
    mutate(ConfirmedForeignNational = ifelse(is.na(ConfirmedForeignNational), 0, ConfirmedForeignNational)) %>%
    rename(StateUt = "State/UnionTerritory") %>%
    mutate(Date = dmy(Date)) %>%
    group_by(StateUt, Date) %>%
    ## Chosing the max number in case there are multiple entries for same date.
    summarize(
      Total =  max(ConfirmedIndianNational) + max(ConfirmedForeignNational),
      Recovered = max(Cured),
      Deceased = max(Deaths),
      Hospitalized = Total-Recovered-Deceased
    ) %>% mutate(Source = "Ministry of Health and Family Welfare")

```