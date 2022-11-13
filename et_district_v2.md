R Notebook
================

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.1.3

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.2 --v ggplot2 3.4.0      v purrr   0.3.4 
    ## v tibble  3.1.8      v dplyr   1.0.10
    ## v tidyr   1.2.1      v stringr 1.4.0 
    ## v readr   2.1.3      v forcats 0.5.1

    ## Warning: package 'ggplot2' was built under R version 4.1.3

    ## Warning: package 'tibble' was built under R version 4.1.3

    ## Warning: package 'tidyr' was built under R version 4.1.3

    ## Warning: package 'readr' was built under R version 4.1.3

    ## Warning: package 'dplyr' was built under R version 4.1.3

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(ggplot2)
```

``` r
districts = read_csv("./data/districts.csv")
```

    ## Rows: 146 Columns: 27-- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (2): system_name, region
    ## dbl (25): system, alg_1, alg_2, bio, chem, ela, eng_1, eng_2, eng_3, math, s...
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
districts
```

    ## # A tibble: 146 x 27
    ##    system system~1 alg_1 alg_2   bio  chem   ela eng_1 eng_2 eng_3  math science
    ##     <dbl> <chr>    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>   <dbl>
    ##  1      0 State o~  70    54.3  65.3  44.2  48.4  71.8  64.8  41.7  54.7    64.5
    ##  2     10 Anderso~  76.1  63.3  73.6  41    45.7  73.7  59.2  38.2  54      64.5
    ##  3     11 Clinton~  NA    NA    NA    NA    58.3  NA    NA    NA    68.9    69.6
    ##  4     12 Oak Rid~  76.9  72    83.5  80.9  56.1  86.7  74.6  53.8  55.3    70.8
    ##  5     20 Bedford~  64.3  42.4  62.1  32.5  44.1  72.3  63.1  44.6  53.1    61.8
    ##  6     30 Benton ~  73.7  58.4  77.1  33.1  46    75.4  60.8  45.6  53.9    65  
    ##  7     40 Bledsoe~  64.8  73.9  73    19.5  35.4  63.6  53.3  50    41.1    56.2
    ##  8     50 Blount ~  73.2  59.8  65.1  45.4  46.3  71.8  66    45.3  50.5    68.4
    ##  9     51 Alcoa C~  82.2  76.8  88    66    50.2  85.5  79.6  67.2  56.6    65.1
    ## 10     52 Maryvil~  83.8  77.3  92.1  80.4  69.6  89.9  82.7  68.1  70.2    87.1
    ## # ... with 136 more rows, 15 more variables: enrollment <dbl>, black <dbl>,
    ## #   hispanic <dbl>, native <dbl>, el <dbl>, swd <dbl>, ed <dbl>,
    ## #   expenditures <dbl>, act_composite <dbl>, chronic_abs <dbl>,
    ## #   suspended <dbl>, expelled <dbl>, grad <dbl>, dropout <dbl>, region <chr>,
    ## #   and abbreviated variable name 1: system_name

There are 146 rows and 27 columns in districts.

Q2. Notice that the first row corresponds to the whole State of
Tennessee. Remove this row and save the result back to districts.

``` r
districts = districts[-1, ]
head(districts)
```

    ## # A tibble: 6 x 27
    ##   system system_~1 alg_1 alg_2   bio  chem   ela eng_1 eng_2 eng_3  math science
    ##    <dbl> <chr>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>   <dbl>
    ## 1     10 Anderson~  76.1  63.3  73.6  41    45.7  73.7  59.2  38.2  54      64.5
    ## 2     11 Clinton ~  NA    NA    NA    NA    58.3  NA    NA    NA    68.9    69.6
    ## 3     12 Oak Ridg~  76.9  72    83.5  80.9  56.1  86.7  74.6  53.8  55.3    70.8
    ## 4     20 Bedford ~  64.3  42.4  62.1  32.5  44.1  72.3  63.1  44.6  53.1    61.8
    ## 5     30 Benton C~  73.7  58.4  77.1  33.1  46    75.4  60.8  45.6  53.9    65  
    ## 6     40 Bledsoe ~  64.8  73.9  73    19.5  35.4  63.6  53.3  50    41.1    56.2
    ## # ... with 15 more variables: enrollment <dbl>, black <dbl>, hispanic <dbl>,
    ## #   native <dbl>, el <dbl>, swd <dbl>, ed <dbl>, expenditures <dbl>,
    ## #   act_composite <dbl>, chronic_abs <dbl>, suspended <dbl>, expelled <dbl>,
    ## #   grad <dbl>, dropout <dbl>, region <chr>, and abbreviated variable name
    ## #   1: system_name

### Q3. How many districts have a proficiency rate of at least 80% for both alg_1 and eng_1?

``` r
districts%>%filter(alg_1 >= 80 & eng_1 >= 80)
```

    ## # A tibble: 13 x 27
    ##    system system~1 alg_1 alg_2   bio  chem   ela eng_1 eng_2 eng_3  math science
    ##     <dbl> <chr>    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>   <dbl>
    ##  1     51 Alcoa C~  82.2  76.8  88    66    50.2  85.5  79.6  67.2  56.6    65.1
    ##  2     52 Maryvil~  83.8  77.3  92.1  80.4  69.6  89.9  82.7  68.1  70.2    87.1
    ##  3    273 Trenton~  91.6  84.7  75.6  64.5  44.6  82.6  76    50.6  62.9    53.6
    ##  4    274 Bradfor~  94.4  92.6  87.9  66.7  56.5  81.8  68.4  70.4  73.4    75.4
    ##  5    275 Gibson ~  83.7  73.2  75.3  63    57.8  83.8  73.5  59.6  67.5    79.7
    ##  6    301 Greenev~  83.2  90.2  77.7  86.1  59.3  87.3  75.1  66    65.5    74.2
    ##  7    390 Henders~  86    88.4  76.4  53.7  53.3  81.1  77.7  51.8  72.1    71.2
    ##  8    793 Arlingt~  88    66.9  82.5  49.8  75.7  88.8  78.1  50.7  75.1    88.3
    ##  9    795 Collier~  90.2  85.6  87.4  80.4  75.1  92.5  86.2  66.2  75.7    86.8
    ## 10    796 Germant~  90    84.2  88.9  78.5  79.4  90.8  87.7  70.8  74.3    88  
    ## 11    822 Kingspo~  87.5  75.5  83.9  71.7  58.5  82.4  77.7  49.7  67.1    75.7
    ## 12    901 Johnson~  86.1  86.4  81.7  65    67.3  82.7  78    63.8  73.7    77.6
    ## 13    940 William~  90.3  84.8  89.2  81    80.7  92.9  88.7  68.6  80.3    91.1
    ## # ... with 15 more variables: enrollment <dbl>, black <dbl>, hispanic <dbl>,
    ## #   native <dbl>, el <dbl>, swd <dbl>, ed <dbl>, expenditures <dbl>,
    ## #   act_composite <dbl>, chronic_abs <dbl>, suspended <dbl>, expelled <dbl>,
    ## #   grad <dbl>, dropout <dbl>, region <chr>, and abbreviated variable name
    ## #   1: system_name

``` r
count(districts%>%filter(alg_1 >= 80 & eng_1 >= 80))
```

    ## # A tibble: 1 x 1
    ##       n
    ##   <int>
    ## 1    13

There are 13 districts.

### Q4. How many districts have a proficiency rate less than 50% for either alg_1 or eng_1?

``` r
districts%>%filter(alg_1 < 50  | eng_1 < 50)
```

    ## # A tibble: 8 x 27
    ##   system system_~1 alg_1 alg_2   bio  chem   ela eng_1 eng_2 eng_3  math science
    ##    <dbl> <chr>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>   <dbl>
    ## 1    240 Fayette ~  39.7  14.7  56.1  20.2  32.6  58.9  53.2  35.4  36.1    41.1
    ## 2    310 Grundy C~  47.9  41.7  51.9  41.9  32.4  62    62    36.7  37.8    47.7
    ## 3    410 Hickman ~  40.2  22.6  54.2  45.1  48.9  60.3  57.5  31.3  58.1    68  
    ## 4    440 Jackson ~  45.9  33.3  68.9  50    42.8  61.8  47.3  46.3  45.3    64.7
    ## 5    480 Lake Cou~  22.9  NA    25    36.5  32.5  36.8  34.6  31.7  34.7    45.6
    ## 6    680 Perry Co~  48.5  50.6  58    19    42.6  60.8  60.6  35.6  61.8    66.5
    ## 7    963 Tenn Sch~  23.1  NA    25    NA     6.7  60    NA    20    NA      10  
    ## 8    985 Achievem~  34    20.4  20.6  NA    14.3  37.8  33     8.2  23.3    26.1
    ## # ... with 15 more variables: enrollment <dbl>, black <dbl>, hispanic <dbl>,
    ## #   native <dbl>, el <dbl>, swd <dbl>, ed <dbl>, expenditures <dbl>,
    ## #   act_composite <dbl>, chronic_abs <dbl>, suspended <dbl>, expelled <dbl>,
    ## #   grad <dbl>, dropout <dbl>, region <chr>, and abbreviated variable name
    ## #   1: system_name

``` r
count(districts%>%filter(alg_1 < 50  | eng_1 < 50))
```

    ## # A tibble: 1 x 1
    ##       n
    ##   <int>
    ## 1     8

There are 8 districts.

### Q5.Which district has the lowest graduation rate?

``` r
districts%>%filter(grad == min(districts$grad, na.rm = TRUE))%>%
  select(system_name, grad)
```

    ## # A tibble: 1 x 2
    ##   system_name            grad
    ##   <chr>                 <dbl>
    ## 1 Tenn School for Blind  11.1

Tennessee School for Blind has the lowest graduation rate.

### Q6. Within the Mid Cumberland region, which district has the highest ACT composite?

``` r
districts%>%filter(region == 'Mid Cumberland')%>%
  filter(act_composite == max(act_composite, na.rm = TRUE))%>%
  select(system_name, act_composite)
```

    ## # A tibble: 1 x 2
    ##   system_name       act_composite
    ##   <chr>                     <dbl>
    ## 1 Williamson County          23.8

### Q7. Create a histogram showing the distribution of graduation rates. What can you say about this distribution?

``` r
ggplot(districts, aes(grad)) +
  geom_histogram(binwidth = 5, fill = 'blue', color = 'black')+
  scale_x_continuous(breaks=seq(0, 100, 10))
```

    ## Warning: Removed 17 rows containing non-finite values (`stat_bin()`).

![](et_district_v2_files/figure-gfm/unnamed-chunk-10-1.png)<!-- --> Most
graduation rates fall between 80-100%. There is one outlier with a
graduation rate 11%.

### Q8. Create a scatter plot to compare alg_1 proficiency rates to alg_2 rates. What do you notice?

### Facet this plot by region. Does anything stand out when you facet the plots?

``` r
ggplot(districts) +
  geom_point(aes(alg_1, alg_2), color = 'blue') +
  scale_x_continuous(breaks=seq(0, 100, 10))
```

    ## Warning: Removed 28 rows containing missing values (`geom_point()`).

![](et_district_v2_files/figure-gfm/unnamed-chunk-11-1.png)<!-- --> The
scatter plot shows there is a strong correlation between alg_1 and alg_2
proficiency rates.

``` r
ggplot(districts) + 
  geom_point(aes(alg_1, alg_2, color = factor(region))) +
  facet_wrap((.~region), nrow = 3, ncol = 3)
```

    ## Warning: Removed 28 rows containing missing values (`geom_point()`).

![](et_district_v2_files/figure-gfm/unnamed-chunk-12-1.png)<!-- --> The
scatter plots show Southwest/Memphis shows the strongest positive
correlation.Southeast shows the weakest correlation. Upper Cumberland
shows a non-linear trend.

### Q9. Create a bar chart showing the total enrollment by region.

### Which region has the highest total enrollment? Which has the smallest?

``` r
options(scipen = 999)
p = ggplot(districts, aes(x=region, y=enrollment, fill = region)) +
  geom_bar(stat = "identity") +
  scale_fill_brewer(palette = "Dark2")

p + coord_flip() 
```

    ## Warning: Removed 4 rows containing missing values (`position_stack()`).

![](et_district_v2_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

Reordering by enrollment

``` r
options(scipen = 999)
p = ggplot(districts, aes(x = reorder(region, +enrollment), y=enrollment, fill = region)) +
  geom_bar(stat = "identity") +
  scale_fill_brewer(palette = "Dark2")

p + coord_flip() 
```

    ## Warning: Removed 4 rows containing missing values (`position_stack()`).

![](et_district_v2_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->
upper cumberland and southwest memphis do not get in order. Mid
Cumberland has the highest enrollment, Northwest has the lowest
enrollment.

### Q10. When creating this bar chart you may have noticed that some districts have missing enrollment values.

### For how many districts is this the case?

``` r
sum(is.na(districts$enrollment))
```

    ## [1] 4

``` r
districts%>%filter(is.na(enrollment))%>%group_by(region, system_name)%>%tally()
```

    ## # A tibble: 4 x 3
    ## # Groups:   region [4]
    ##   region            system_name                   n
    ##   <chr>             <chr>                     <int>
    ## 1 East TN           Tenn School for Deaf          1
    ## 2 Mid Cumberland    Tenn School for Blind         1
    ## 3 Southwest/Memphis West Tenn School for Deaf     1
    ## 4 Upper Cumberland  Alvin C. York Institute       1

### Q11. What is the mean graduation rate across all districts?

### What might be wrong with using just the regular mean to assess average graduation rates?

``` r
mean(districts$grad, na.rm = TRUE)
```

    ## [1] 90.06562

Enrollment can affect graduation rate, schools with smaller enrollment
are easily influenced by dropouts, so have smaller graduation rates
which may skew data downwards.

### Q12. Redo the previous question but use a weighted average (weighted.mean) graduation across all districts, weighing by enrollment.

### How much does this change your answer?

### Can you explain using the data the reason for the big change from using the mean?

``` r
weighted.mean(districts$grad, dplyr::coalesce(districts$enrollment,0), na.rm=TRUE)
```

    ## [1] 87.33285
