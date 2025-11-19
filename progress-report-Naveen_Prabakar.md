
# Lab report \#4

``` r
#Gather the HTML of the data being scrapped

url <- "https://www.baseball-reference.com/awards/hof_2025.shtml"
html <- read_html(url)
html
```

    ## {html_document}
    ## <html data-version="klecko-" data-root="/home/br/build" lang="en" class="no-js">
    ## [1] <head>\n<meta http-equiv="Content-Type" content="text/html; charset=UTF-8 ...
    ## [2] <body class="br">\n<div id="wrap">\n  <div id="header" role="banner">\n   ...

``` r
#Gather all the tables from the HTML dataset

tables <- html %>% html_table(fill=TRUE)
tables
```

    ## [[1]]
    ## # A tibble: 29 × 39
    ##    ``    ``          ``    ``    ``    ``    ``    ``    ``    ``    ``    ``   
    ##    <chr> <chr>       <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr>
    ##  1 Rk    Name        YoB   Votes %vote HOFm  HOFs  Yrs   WAR   WAR7  JAWS  Jpos 
    ##  2 1     Ichiro Suz… 1st   393   99.7% 235   44    19    60.0  43.7  51.8  56.0 
    ##  3 2     CC Sabathia 1st   342   86.8% 128   48    19    62.3  39.4  50.8  61.3 
    ##  4 3     Billy Wagn… 10th  325   82.5% 107   24    16    27.7  19.8  23.7  31.6 
    ##  5 4     Carlos Bel… 3rd   277   70.3% 126   52    20    70.0  44.4  57.2  58.0 
    ##  6 5     Andruw Jon… 8th   261   66.2% 109   34    17    62.7  46.4  54.6  58.0 
    ##  7 6     Chase Utley 2nd   157   39.8% 94    36    16    64.6  49.3  56.9  57.0 
    ##  8 7     Alex Rodri… 4th   146   37.1% 390   77    22    117.4 64.3  90.8  55.4 
    ##  9 8     Manny Rami… 9th   135   34.3% 226   69    19    69.3  40.0  54.6  53.5 
    ## 10 9     Andy Petti… 7th   110   27.9% 128   44    18    60.2  34.1  47.2  61.3 
    ## # ℹ 19 more rows
    ## # ℹ 27 more variables: `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Pitching Stats` <chr>,
    ## #   `Pitching Stats` <chr>, `Pitching Stats` <chr>, `Pitching Stats` <chr>, …
    ## 
    ## [[2]]
    ## # A tibble: 3 × 38
    ##   ``    ``          ``    ``      ``    ``    ``    ``    ``    ``    ``   
    ##   <chr> <chr>       <chr> <chr>   <chr> <chr> <chr> <chr> <chr> <chr> <chr>
    ## 1 Rk    Name        Votes "%vote" HOFm  HOFs  Yrs   WAR   WAR7  JAWS  Jpos 
    ## 2 1     Dave Parker 14    ""      125   42    19    40.1  37.4  38.7  56.0 
    ## 3 2     Dick Allen  13    ""      99    39    15    58.8  45.9  52.4  56.1 
    ## # ℹ 27 more variables: `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Pitching Stats` <chr>,
    ## #   `Pitching Stats` <chr>, `Pitching Stats` <chr>, `Pitching Stats` <chr>,
    ## #   `Pitching Stats` <chr>, `Pitching Stats` <chr>, `Pitching Stats` <chr>, …

``` r
# Filter for only the voting table
votes <- tables[[1]]
head(votes)
```

    ## # A tibble: 6 × 39
    ##   ``    ``           ``    ``    ``    ``    ``    ``    ``    ``    ``    ``   
    ##   <chr> <chr>        <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr>
    ## 1 Rk    Name         YoB   Votes %vote HOFm  HOFs  Yrs   WAR   WAR7  JAWS  Jpos 
    ## 2 1     Ichiro Suzu… 1st   393   99.7% 235   44    19    60.0  43.7  51.8  56.0 
    ## 3 2     CC Sabathia  1st   342   86.8% 128   48    19    62.3  39.4  50.8  61.3 
    ## 4 3     Billy Wagner 10th  325   82.5% 107   24    16    27.7  19.8  23.7  31.6 
    ## 5 4     Carlos Belt… 3rd   277   70.3% 126   52    20    70.0  44.4  57.2  58.0 
    ## 6 5     Andruw Jones 8th   261   66.2% 109   34    17    62.7  46.4  54.6  58.0 
    ## # ℹ 27 more variables: `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Batting Stats` <chr>,
    ## #   `Batting Stats` <chr>, `Batting Stats` <chr>, `Pitching Stats` <chr>,
    ## #   `Pitching Stats` <chr>, `Pitching Stats` <chr>, `Pitching Stats` <chr>,
    ## #   `Pitching Stats` <chr>, `Pitching Stats` <chr>, `Pitching Stats` <chr>, …

``` r
# Build the data frame]
actual_col_names <- votes[1, ]
colnames(votes) <- actual_col_names
votes <- votes[-1, ]
```

``` r
#Save the data frame (the intial Data)
write.csv(votes, "C:\\Users\\nvnpr\\Downloads\\voting.csv")
```

``` r
#Preview of the saved Data from the scrapped data
head(votes)
```

    ## # A tibble: 6 × 39
    ##   Rk    Name       YoB   Votes `%vote` HOFm  HOFs  Yrs   WAR   WAR7  JAWS  Jpos 
    ##   <chr> <chr>      <chr> <chr> <chr>   <chr> <chr> <chr> <chr> <chr> <chr> <chr>
    ## 1 1     Ichiro Su… 1st   393   99.7%   235   44    19    60.0  43.7  51.8  56.0 
    ## 2 2     CC Sabath… 1st   342   86.8%   128   48    19    62.3  39.4  50.8  61.3 
    ## 3 3     Billy Wag… 10th  325   82.5%   107   24    16    27.7  19.8  23.7  31.6 
    ## 4 4     Carlos Be… 3rd   277   70.3%   126   52    20    70.0  44.4  57.2  58.0 
    ## 5 5     Andruw Jo… 8th   261   66.2%   109   34    17    62.7  46.4  54.6  58.0 
    ## 6 6     Chase Utl… 2nd   157   39.8%   94    36    16    64.6  49.3  56.9  57.0 
    ## # ℹ 27 more variables: G <chr>, AB <chr>, R <chr>, H <chr>, HR <chr>,
    ## #   RBI <chr>, SB <chr>, BB <chr>, BA <chr>, OBP <chr>, SLG <chr>, OPS <chr>,
    ## #   `OPS+` <chr>, W <chr>, L <chr>, ERA <chr>, `ERA+` <chr>, WHIP <chr>,
    ## #   G <chr>, GS <chr>, SV <chr>, IP <chr>, H <chr>, HR <chr>, BB <chr>,
    ## #   SO <chr>, `Pos Summary` <chr>

``` r
# Preview of the Lahman Data
head(HallOfFame)
```

    ##    playerID yearID votedBy ballots needed votes inducted category needed_note
    ## 1 aaronha01   1982   BBWAA     415    312   406        Y   Player        <NA>
    ## 2 abbotji01   2005   BBWAA     516    387    13        N   Player        <NA>
    ## 3 abreubo01   2020   BBWAA     397    298    22        N   Player        <NA>
    ## 4 abreubo01   2021   BBWAA     401    301    35        N   Player        <NA>
    ## 5 abreubo01   2022   BBWAA     394    296    34        N   Player        <NA>
    ## 6 abreubo01   2023   BBWAA     389    292    60        N   Player        <NA>

``` r
#Clean the data

votes <- votes |> select(Rk, Name, YoB, Votes, `%vote`, HOFm, HOFs, Yrs, WAR, WAR7, JAWS)

votes <- votes |> mutate(`%vote` = parse_number(`%vote`),across(c(Rk, YoB, Votes, HOFm, HOFs, Yrs, WAR, WAR7, JAWS), as.numeric),Name = str_trim(Name))
```

    ## Warning: There was 1 warning in `mutate()`.
    ## ℹ In argument: `across(c(Rk, YoB, Votes, HOFm, HOFs, Yrs, WAR, WAR7, JAWS),
    ##   as.numeric)`.
    ## Caused by warning:
    ## ! NAs introduced by coercion

``` r
# Join the dataset to get player ID:

votes <- votes |>left_join(Lahman::People |>  mutate(fullName = paste(nameFirst, nameLast)) |> select(playerID, fullName),by = c("Name" = "fullName"))
```

``` r
#  Add yearID
votes <- votes |> mutate(yearID = 2025)

# Add votedBy
votes <- votes |> mutate(votedBy = "BBWAA")

#  Calculate total ballots
votes <- votes |> mutate(Votes = as.numeric(Votes))  
votes <- votes |> mutate(votes = Votes)               
votes <- votes |> mutate(ballots = max(votes, na.rm = TRUE))

#  Calculate needed votes (75% of ballots)
votes <- votes |> mutate(needed = round(0.75 * ballots))

#  Determine inducted status
votes <- votes |> mutate(inducted = if_else(`%vote` >= 75, "Y", "N"))

#  Add category column
votes <- votes |> mutate(category = "Player")


#  Select only the final columns
votes <- votes |>
  select(playerID, yearID, votedBy, ballots, needed,
         votes, inducted, category)


votes
```

    ## # A tibble: 28 × 8
    ##    playerID  yearID votedBy ballots needed votes inducted category
    ##    <chr>      <dbl> <chr>     <dbl>  <dbl> <dbl> <chr>    <chr>   
    ##  1 suzukic01   2025 BBWAA       393    295   393 Y        Player  
    ##  2 sabatcc01   2025 BBWAA       393    295   342 Y        Player  
    ##  3 wagnebi02   2025 BBWAA       393    295   325 Y        Player  
    ##  4 <NA>        2025 BBWAA       393    295   277 N        Player  
    ##  5 jonesan01   2025 BBWAA       393    295   261 N        Player  
    ##  6 utleych01   2025 BBWAA       393    295   157 N        Player  
    ##  7 rodrial01   2025 BBWAA       393    295   146 N        Player  
    ##  8 ramirma02   2025 BBWAA       393    295   135 N        Player  
    ##  9 pettian01   2025 BBWAA       393    295   110 N        Player  
    ## 10 <NA>        2025 BBWAA       393    295    81 N        Player  
    ## # ℹ 18 more rows
