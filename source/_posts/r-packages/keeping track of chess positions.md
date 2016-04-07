---
title: "How can chess positions be kept track of?"
author: "Josh Merrell"
date: "April 7, 2016"
commments: true
tags: 
- R Packages
- Analytics
- Chess
categories: 
- R Packages
---

I keep track of chess positions using a data frame of 64 variables, one for each square of the chessboard. An example of an empty chessboard can be generated with the *empty* function:


```r
load("chessDoodles.RData")

position <- empty(gameName = "example")
position
```

```
##               a8 a7 a6 a5 a4 a3 a2 a1 b8 b7 b6 b5 b4 b3 b2 b1 c8 c7 c6 c5
## example_empty NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
##               c4 c3 c2 c1 d8 d7 d6 d5 d4 d3 d2 d1 e8 e7 e6 e5 e4 e3 e2 e1
## example_empty NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
##               f8 f7 f6 f5 f4 f3 f2 f1 g8 g7 g6 g5 g4 g3 g2 g1 h8 h7 h6 h5
## example_empty NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
##               h4 h3 h2 h1
## example_empty NA NA NA NA
```

Note that columns are named after squares of the chessboard, and rows are named in gameName_move format. An example of a chessboard where the pieces have not been moved can be generated with the *setup* function (which internally calls the *empty* function):


```r
position <- setup(gameName = "game1")
position[,c("d1","e1","d8","e8")]
```

```
##                      d1         e1          d8         e8
## game1_empty        <NA>       <NA>        <NA>       <NA>
## game1_zero  white Queen white King black Queen black King
```

The position object is built row-by-row using the *newPosition* function.


```r
newRow <- newPosition(new_pgn = "game1_1.e4", startPosition = nrow(position))
position <- rbind(position,newRow)
position[,c("e2","e4")]
```

```
##                     e2         e4
## game1_empty       <NA>       <NA>
## game1_zero  white pawn       <NA>
## game1_1.e4        <NA> white pawn
```

This *position* object is referenced by all the position-oriented functions I have written.
