---
title: "Test tabs"
output: html_document
---

`r knitr::opts_chunk$set(echo = FALSE, warning = FALSE, message = FALSE, cache = F)`

```{r}
library(highcharter)
library(tidyverse)
# This empty chart is necessary to initialize Highcharter in the tabs
highchart(height = 1)
```


```{r, results = 'asis'}
cat('## Tabs panel {.tabset}   \n')
invisible(
  iris %>% 
      dplyr::group_split(Species) %>% 
      purrr::imap(.,~{
        # create tabset for each group 
        cat('### Tab',.y,'   \n')
        cat('\n')
        p <- hchart(.x,"scatter", hcaes(x = Sepal.Length, y = Sepal.Width))
        cat(as.character(htmltools::tagList(p)))
      })
)
