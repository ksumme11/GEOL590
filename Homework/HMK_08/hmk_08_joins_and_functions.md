# HMK 08

# Joins

To prepare for Question 1, load packages and create flights2:

``` r
library(tidyverse)
library(nycflights13)

flights2 <- flights |>
  select(year, time_hour, origin, dest, tailnum, carrier)
```

1.  Imagine you’ve found the top 10 most popular destinations using this
    code:

``` r
top_dest <- flights2 |>
  count(dest, sort = TRUE) |>
  head(10)
```

How can you find all flights to those destinations?

To find all the flights to those destinations, I can use the left_join
function to combine the top_dest data set with the larger flights2 data
set and join only according to dest. I added count(dest, sort = TRUE) to
make sure my output was in the same order as the top_dest output.

``` r
all_flights <- top_dest |>
  left_join(flights2, by = "dest") |>
  count(dest, sort = TRUE) 
```

I used nrow() to ensure my all_flights had the correct number of rows.

``` r
nrow(all_flights)
```

    [1] 10

To be extra certain that they matched, I used the count() function to
compare the flights listed in all_flights vs top_dest.

``` r
all_flights |> count(dest)
```

    # A tibble: 10 × 2
       dest      n
       <chr> <int>
     1 ATL       1
     2 BOS       1
     3 CLT       1
     4 DCA       1
     5 FLL       1
     6 LAX       1
     7 MCO       1
     8 MIA       1
     9 ORD       1
    10 SFO       1

# Functions

2.  Write a function to ‘rescale’ a numeric vector by subtracting the
    mean of the vector from each element and then dividing each element
    by the standard deviation.

``` r
r <- c(1:25)

rescale <- function(x) {
  x - mean(x) / sd(x)
}

r2 <- rescale(r)
```

I created a vector of the valued 1-25, which are assigned as an object
(r). I chose a name for the function, which i called “rescale,” then I
listed the arguments to the function inside function. The argument was
to subtract the mean of x from x, then divide each value by the standard
deviation of x. The argument code is within the body of the function,
represented by a { that immediately follows function(). To rescale r I
created the object r2 and used rescale() to apply the arguments to that
object.
