Activity 3
================
Bruce Buurstra

Today you will be creating and manipulating vectors, lists, and data
frames to uncover a top secret message.

As you work through this document with your Team members, remember to:

-   Ask questions
-   Google is your friend! If an error is confusing, copy it into Google
    and see what other people are saying. If you don’t know how to do
    something, search for it.
-   Just because there is no error message doesn’t mean everything went
    smoothly. Use the console to check each step and make sure you have
    accomplished what you wanted to accomplish.

Do not edit this first R code chunk. This will allow you to knit your
document and view errors within the knitted report.

### Setup

Each of the following R chunks will cause an error and/or do the desired
task incorrectly. Find the mistake, and correct it to complete the
intended action.

Create three vectors that contain: 1) the lower case letters, 2) the
upper case letters, and 3) some punctuation marks.

``` r
lower_case <- c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z")

upper_case <- c("A", "B", "C", "D", "E", "F", "G", "H","I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z")

punctuation <- c(".", ",", "!", "?", "'", "\"" ,"(", ")", " ", "-", ";", ":")
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: It took me a long time to spot the missing comma in the
uppercase vector. I had to google how to get the " mark to show inside
quotation marks.

Make one long vector containing all the symbols.

``` r
my_symbols <- c(lower_case, upper_case, punctuation)
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: I looked at the dataset and seen the number of punctuation
values were not matching the same number of values as upper\_case and
lower\_case so it was getting messed up. It also was making a data frame
with 3 vectors by looking at it and we only want one long vector so I
used c instead of cbind.

Turn the `my_symbols` vector into a data frame, with the variable name
“Symbol”.

``` r
my_symbols <- data.frame(my_symbols)
names(my_symbols) = "Symbol"
my_symbols
```

    ##    Symbol
    ## 1       a
    ## 2       b
    ## 3       c
    ## 4       d
    ## 5       e
    ## 6       f
    ## 7       g
    ## 8       h
    ## 9       i
    ## 10      j
    ## 11      k
    ## 12      l
    ## 13      m
    ## 14      n
    ## 15      o
    ## 16      p
    ## 17      q
    ## 18      r
    ## 19      s
    ## 20      t
    ## 21      u
    ## 22      v
    ## 23      w
    ## 24      x
    ## 25      y
    ## 26      z
    ## 27      A
    ## 28      B
    ## 29      C
    ## 30      D
    ## 31      E
    ## 32      F
    ## 33      G
    ## 34      H
    ## 35      I
    ## 36      J
    ## 37      K
    ## 38      L
    ## 39      M
    ## 40      N
    ## 41      O
    ## 42      P
    ## 43      Q
    ## 44      R
    ## 45      S
    ## 46      T
    ## 47      U
    ## 48      V
    ## 49      W
    ## 50      X
    ## 51      Y
    ## 52      Z
    ## 53      .
    ## 54      ,
    ## 55      !
    ## 56      ?
    ## 57      '
    ## 58      "
    ## 59      (
    ## 60      )
    ## 61       
    ## 62      -
    ## 63      ;
    ## 64      :

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: dataframe was not found so I searched and found the actual
function is data.frame. Also putting quotation marks around Symbol made
it the column name in the data frame.

Find the total number of symbols we have in our data frame.

``` r
len <- length(my_symbols$Symbol)
len
```

    ## [1] 64

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: Length was returning a value of 1, the total number of
columns, looking at the column instead we got a length of 64 to return
the number of rows which is correct.

5.  Create a new variable in your dataframe that assigns a number to
    each symbol.

``` r
my_symbols$Num <- 1:len
```

Comment on what you noticed about the errors and how you used this
information to correct the issues.

**Response**: I know that a dollar symbol is what is used for columns
not a percent symbol.

![](README-img/noun_pause.png) **Planned Pause Point**: If things made
sense, feel free to continue on while you wait. Otherwise, contact your
instructor to have them verify your work.

### Decoding the secret message.

This chunk will load up the encoded secret message data and assign it as
a vector. There are no errors here.

``` r
# Read in full csv file
top_secret <- readr::read_csv("data/secret_code.csv", col_names = FALSE)
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   X1 = col_double()
    ## )

``` r
# Pick off only the column X1
top_secret <- top_secret$X1
```

By altering this top secret set of numbers, you will be able to create a
message. Write your own code to complete the steps below.

1.  Add 14 to every number.
2.  Multiply every number by 18, then subtract 257.
3.  Exponentiate every number. (That is, do e ^ \[each number\]. You may
    need to Google how to this!)
4.  Square every number.

``` r
top_secret_addition <- top_secret + 14
top_secret_mult_sub <- (top_secret_addition*18) - 257
top_secret_exp <- exp(top_secret_mult_sub)
top_secret_square <- top_secret_exp^2
```

**HQ UPDATE:** Headquarters has informed you that at this stage of
decoding, there should be 496 numbers in the secret message that are
below 17.

5.  Turn your vector of numbers into a matrix with 5 columns.
6.  Separately from your top secret numbers, create a vector of all the
    even numbers between 1 and 502. Name it “`evens`”. That is, `evens`
    should be an R object that contain the values 2, 4, 6, 8, …, 502.
7.  Subtract the “evens” vector from the first column of your secret
    message matrix.
8.  Subtract 100 from all numbers 18-24th rows of the 3rd column.
9.  Multiply all numbers in the 4th and 5th column by 2.
10. Turn your matrix back into a vector.

``` r
my_matrix <- matrix(top_secret_square,ncol = 5)
my_matrix[,1]
```

    ##   [1]   43   12   67   33   15   13   22   77   53   34   83   56   44   29   44
    ##  [16]   35   39   97   39  101   61   55   55   62   64   77  115   69   59   74
    ##  [31]  123   68   75   73   74  133   89  112 3799   81 3803   88  167  137 3811
    ##  [46]  108  175  457  123  101  463  129 3827  637  191 1633  178 3837  119 3841
    ##  [61]  266  205 1647 1649  274  157 3855  332  139  309  167 3865  930  773 3871
    ##  [76]  161  218  157  354  169  187 3885  230  249  531 3893  223  257  502  324
    ##  [91]  218  508  267  213  386  208 3915  205  199  369  227 3925  207  217  534
    ## [106]  437  575  577 3939  221 3943  420  251  253  246  376  259 3957  239  436
    ## [121]  258 3965  607  473  475  448 3975  617  322  285 3983  280  347  284 3991
    ## [136] 1793  338  301 3999  641  283  453  311 4009 1019 1813 4015  360  523  469
    ## [151]  327 4025 1827  372  335  636  339 4037  319  644  347 4045  687  353  814
    ## [166]  357  530 1857  363  365  538 4188  971  373  351  676 4198  581  502  376
    ## [181] 4083  368  591  993  731 4093  375  572  394 4101 1903  448  411  469  714
    ## [196] 4113  475  412  423  401 4123  629  442 4129  446  853  610 4137 1643  781
    ## [211] 4143  428  451  509  626  481 4155  517  634 4161  443 4165  495  449  646
    ## [226]  501 4175  465  459  604  606  489  482 4189 2586  536  499 4197 1378  561
    ## [241]  843  493  567  744  634  517  855 3412 4219  564  583

``` r
evens <-c(seq(2,502,2))
subtract <- my_matrix[,1]-evens
```

**HQ UPDATE:** Headquarters has informed you that at this stage of
decoding, all numbers in indices 500 and beyond are below 100.

11. Take the square root of all numbers in indices 38 to 465.
12. Round all numbers to the nearest whole number.
13. Replace all instances of the number 39 with 20.

**HQ UPDATE:** Headquarters has informed you that your final message
should have 421 even numbers.

![](README-img/noun_pause.png) **Planned Pause Point**: If things made
sense, feel free to continue on while you wait. Otherwise, contact your
instructor to have them verify your work.

## The secret message!

Use your final vector of numbers as indices for `my_symbols` to discover
the final message, by running the following code:

``` r
stringr::str_c(my_symbols$Symbol[top_secret], collapse = "")
```

    ## [1] ""

Google the first line of this message, if you do not recognize it, to
see what it is.

**delete this line and comment on what on the activity as a whole**

Comment on what you noticed about the activity as a whole.

**Response**:

Push your updated report to your `<username>` branch - you are done with
this `.Rmd` file and can go back to the README directions while you wait
for you Team Members.

## Attribution

This activity is based on a lab from [Dr. Kelly
Bodwin](https://www.kelly-bodwin.com/)’s Stat 331 course
