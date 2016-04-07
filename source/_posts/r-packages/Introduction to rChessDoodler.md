---
title: "Introduction to ChessDoodle Functions"
author: "Josh Merrell"
date: "March 30, 2016"
commments: true
tags: 
- R Packages
- Analytics
- Chess
categories: 
- R Packages
---

[This workspace](https://github.com/brantmerrell/chessdoodles/blob/master/chessDoodles.RData) is being developed into a package geared to help the user to explore and think about the chessboard.


```r
# clear workspace
rm(list=ls())

# load workspace
load("chessDoodles.RData")
```

The regex patterns interpret strings. 


```r
ls(pattern = "Pattern")
```

```
##  [1] "bishopPattern"    "blackPattern"     "capturePattern"  
##  [4] "castlePattern"    "castleQPattern"   "checkmatePattern"
##  [7] "checkPattern"     "colorPatterns"    "kingPattern"     
## [10] "knightPattern"    "pawnPattern"      "pgnPattern"      
## [13] "piecePatterns"    "queenPattern"     "rookPattern"     
## [16] "whitePattern"
```

The pathPrior() function is named after the term *a priori*. For a given input piece and square of the chessboard, it returns the *path* the piece can take on an empty chessboard, *prior* to the circumstance that arise when a game is in play.


```r
pathPrior(piece = "bishop", square = "e5")
```

```
##  [1] "a1" "b2" "b8" "c3" "c7" "d4" "d6" "f6" "f4" "g7" "g3" "h8" "h2"
```

```r
pathPrior(piece = "knight", square = "e5")
```

```
## [1] "f7" "d7" "f3" "d3" "g6" "c6" "g4" "c4"
```

The pawn is the only piece unable to move backwards, and its *direction* depends on its color.


```r
pathPrior(piece = "black pawn", square = "e5")
```

```
## [1] "e4" "d4" "f4"
```

```r
pathPrior(piece = "white pawn", square = "e5")
```

```
## [1] "e6" "d6" "f6"
```

It is the only piece whose color needs to be specified for pathPrior.() to work effectively. *Post.()* functions are conversely named after the term *a posteriori*. They trim each piece's options according to the circumstances of the entire board. 


```r
ls(pattern = "Post")
```

```
## [1] "bishopPost."   "kingPost."     "knightPost."   "mobilityPost."
## [5] "pathPost."     "pawnPost."     "piecePost."    "queenPost."   
## [9] "rookPost."
```

They cannot be used unless a snapshot of the chessboard's position exists for them to analyze. The snapshots exist as rows of the *position* data frame, which has one variable for each square of the chessboard. Each variable in *position* is a square of the chessboard,


```r
colnames(position)
```

```
##  [1] "a8" "a7" "a6" "a5" "a4" "a3" "a2" "a1" "b8" "b7" "b6" "b5" "b4" "b3"
## [15] "b2" "b1" "c8" "c7" "c6" "c5" "c4" "c3" "c2" "c1" "d8" "d7" "d6" "d5"
## [29] "d4" "d3" "d2" "d1" "e8" "e7" "e6" "e5" "e4" "e3" "e2" "e1" "f8" "f7"
## [43] "f6" "f5" "f4" "f3" "f2" "f1" "g8" "g7" "g6" "g5" "g4" "g3" "g2" "g1"
## [57] "h8" "h7" "h6" "h5" "h4" "h3" "h2" "h1"
```

and each observation is a snapshot of the game:


```r
set.seed(123); 
position[sample(2:nrow(position),1), 
         sample(1:ncol(position),10)]
```

```
##            c6         g7         d7   g3         h8   a6         d2   g6
## 000_zero <NA> black pawn black pawn <NA> black Rook <NA> white pawn <NA>
##                  h7   h3
## 000_zero black pawn <NA>
```

The first row is the *empty* chessboard, with no pieces listed for any of the squares. The second row is the *zero* position, with pieces set at starting positions.  

We can compare the mobility of a white knight on b1 before and after the pieces are set up:


```r
pathPrior(piece = "knight", square = "b1")
```

```
## [1] "c3" "a3" "d2"
```

```r
pathPost.(square = "b1", game_pgn = "000_zero")
```

```
## [1] "c3" "a3"
```

Because of the game_pgn input, *pathPost.* knows that the piece on h2 is a white knight, and that it cannot move to **d2** because that space is occupied by another pawn.

Let us begin by observing the [game](https://www.chess.com/echess/game?id=131764454) I am currently playing. We can modify the link into the format *"http://username:password@chess.com/..."* and pass it to the *rawToTidy()* function as follows:


```r
LinkID <- 131764454
Username <- "thinkboolean"
Password <- "blogChess" # counting on you not to abuse this; feel free to contact me for details
Link <- paste("http://",
              Username,
              ":",
              Password,
              "@chess.com/echess/game?id=",
              LinkID)
print(Link)
```

```
## [1] "http:// thinkboolean : blogChess @chess.com/echess/game?id= 131764454"
```

```r
games <- rawToTidy(Link)
print(games)
```

```
##                                                   Title
## 1 risoarcher vs thinkboolean - Online Chess - Chess.com
##                                                                                    pgn
## 1 1.e4 e5 2.f4 exf4 3.d4 Qe7 4.Bxf4 Qxe4 5.Qe2 Qxe2 6.Bxe2 d6 7.Nf3 Nc6 8.a3 Nf6 9.Nc3
```

Now we can expand this pgn from a single string to a data frame of moves using *tidyToPgn()*.


```r
moves <- as.data.frame(tidyToPgn(games,n=1, string = "xmpl"))
print(moves)
```

```
##    gameID      pgn
## 1   xmpl1     1.e4
## 2   xmpl1   1...e5
## 3   xmpl1     2.f4
## 4   xmpl1 2...exf4
## 5   xmpl1     3.d4
## 6   xmpl1  3...Qe7
## 7   xmpl1   4.Bxf4
## 8   xmpl1 4...Qxe4
## 9   xmpl1    5.Qe2
## 10  xmpl1 5...Qxe2
## 11  xmpl1   6.Bxe2
## 12  xmpl1   6...d6
## 13  xmpl1    7.Nf3
## 14  xmpl1  7...Nc6
## 15  xmpl1     8.a3
## 16  xmpl1  8...Nf6
## 17  xmpl1    9.Nc3
```

The first move is pawn to e4. Inputing it into the *newPosition()* function replicates the last (or specified) row of the *position* frame, places the white pawn on e4, and removes it from e2.


```r
position[,c("e2","e4")]
```

```
##                   e2   e4
## 000_empty       <NA> <NA>
## 000_zero  white pawn <NA>
```

```r
newPosition(new_pgn = "1.e4", 
            startPosition = nrow(position))[,
                                            c("e2","e4")]
```

```
##      e2         e4
## 1.e4 NA white pawn
```

newPosition() is designed to sequentially build on the *position* object. 


```r
for(n in 1:nrow(moves)){
  pgn <- paste("xmpl1",
               as.vector(moves[n,"pgn"]),
               sep="_")
  if(!pgn %in% row.names(position)){
    position<-rbind(position, newPosition(new_pgn = pgn))
  }
}
rownames(position)
```

```
##  [1] "000_empty"      "000_zero"       "xmpl1_1.e4"     "xmpl1_1...e5"  
##  [5] "xmpl1_2.f4"     "xmpl1_2...exf4" "xmpl1_3.d4"     "xmpl1_3...Qe7" 
##  [9] "xmpl1_4.Bxf4"   "xmpl1_4...Qxe4" "xmpl1_5.Qe2"    "xmpl1_5...Qxe2"
## [13] "xmpl1_6.Bxe2"   "xmpl1_6...d6"   "xmpl1_7.Nf3"    "xmpl1_7...Nc6" 
## [17] "xmpl1_8.a3"     "xmpl1_8...Nf6"  "xmpl1_9.Nc3"
```

These functions will provide the analytic muscle for future blogging analyses. 
