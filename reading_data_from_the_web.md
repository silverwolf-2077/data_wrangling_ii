reading_data_from_the_web
================
Ruihan Ding
2025-10-21

Import NSDUH data

``` r
url = "https://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

drug_use = read_html(url)
```

This is an “easy” case

``` r
nsduh_df = 
  drug_use |> 
  html_table() |> 
  first() |>  # = nth(1)
  slice(-1) # remove the first row
```

Slightly harder case

``` r
url = "https://www.imdb.com/list/ls070150896/"

sw_html = read_html(url)
```

Now pull out elements of the html that I care about

``` r
title_vec = 
  sw_html |> 
  html_elements(".ipc-title-link-wrapper .ipc-title__text--reduced") |> 
  html_text()

metascore_vec = 
  sw_html |> 
  html_elements(".metacritic-score-box") |> 
  html_text()

runtime_vec = 
  sw_html |> 
  html_elements(".dli-title-metadata-item:nth-child(2)") |> 
  html_text()

sw_df = 
  tibble(
    title = title_vec,
    metascore = metascore_vec,
    runtime = runtime_vec
  )
```
