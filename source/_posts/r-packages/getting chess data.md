---
title: "How can the data for a game be obtained and neatened?"
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


I built this package for compatibility with [chess.com](https://www.chess.com/), so contact me if you want me to use it for other sources. Everything required for this demo can be found in [my chessDoodles workspace](https://github.com/brantmerrell/chessdoodles/blob/master/chessDoodles.RData)


```r
# clear workspace
rm(list=ls())

# load workspace
load("chessDoodles.RData")
```

A link to a chess.com game always ends with a game ID. Here are two examples:
 - [https://www.chess.com/echess/game?id=127609996](https://www.chess.com/echess/game?id=127609996)
 - [https://www.chess.com/echess/game?id=131764454](https://www.chess.com/echess/game?id=131764454)

So the ID of the game to assess can be used to construct the link to the game.


```r
linkIDs <- c(127609996, 131764454)

Links <- paste("chess.com/echess/game?id=",
               linkIDs,
               sep = "")
Links
```

```
## [1] "chess.com/echess/game?id=127609996"
## [2] "chess.com/echess/game?id=131764454"
```

These games can be viewed publicly, but scraping the [pgn](https://en.wikipedia.org/wiki/Portable_Game_Notation) for each requires a username and password. I think it's easiest to embed the password into the link with the format *"http://username:password@chess.com/..."*.


```r
# store username and password
Username <- "thinkboolean"
Password <- "blogChess" # counting on you not to abuse this; feel free to contact me for details

# finish constructing links
Links <- paste("http://",
               Username,
               ":",
               Password,
               "@",
               Links, 
               sep = "")
Links
```

```
## [1] "http://thinkboolean:blogChess@chess.com/echess/game?id=127609996"
## [2] "http://thinkboolean:blogChess@chess.com/echess/game?id=131764454"
```

The *rawToTidy* function scrapes the title and pgn of a chessLink.


```r
games <- rawToTidy(Links[1])
for(Link in Links[-1]){
  games <- rbind(games, rawToTidy(Link))
}
games
```

```
##                                                   Title
## 1 thinkboolean vs risoarcher - Online Chess - Chess.com
## 2 risoarcher vs thinkboolean - Online Chess - Chess.com
##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         pgn
## 1 1.e4 e5 2.Qf3 Nc6 3.b3 Nf6 4.Nc3 d6 5.Bc4 Nd4 6.Qd3 Bg4 7.Nge2 Bxe2 8.Nxe2 Nxe2 9.Qxe2 Be7 10.Qf3 O-O 11.Bb2 c5 12.O-O Qd7 13.a4 a6 14.Rfe1 b5 15.axb5 axb5 16.Rxa8 Rxa8 17.h4 Qg4 18.Bd5 Qxf3 19.gxf3 Nxd5 20.exd5 Bxh4 21.Re4 Bg5 22.d3 Ra2 23.Bc3 Bf6 24.Re2 g5 25.Kg2 Kg7 26.Be1 h5 27.Kg3 Kg6 28.b4 c4 29.dxc4 bxc4 30.b5 Rb2 31.Re4 Rxb5 32.Rxc4 Rxd5 33.Bb4 Rd4 34.Rxd4 exd4 35.Bxd6 Kf5 36.Bb4 Be5 37.Kg2 Kf4 38.Bd2 Kf5 39.Kh3 f6 40.Kg2 Bf4 41.Bb4 Be5 42.Kf1 g4 43.fxg4 hxg4 44.Ke2 Ke4 45.Kd1
## 2                                                                                                                                                                                                                                                                                                                                                                                                         1.e4 e5 2.f4 exf4 3.d4 Qe7 4.Bxf4 Qxe4 5.Qe2 Qxe2 6.Bxe2 d6 7.Nf3 Nc6 8.a3 Nf6 9.Nc3 Bf5 10.O-O-O
```

This provides a data frame in which each row is a game. The *tidyToPgn* function can split a game into a move-by-move data frame. 


```r
# first game:
moves <- tidyToPgn(tidyDF = games, n=1)

# other games:
for(n in 2:length(games)){
  moves <- rbind(moves, tidyToPgn(tidyDF = games, n = n))
}
head(moves)
```

```
##      gameID  pgn      
## [1,] "beta1" "1.e4"   
## [2,] "beta1" "1...e5" 
## [3,] "beta1" "2.Qf3"  
## [4,] "beta1" "2...Nc6"
## [5,] "beta1" "3.b3"   
## [6,] "beta1" "3...Nf6"
```

```r
tail(moves)
```

```
##        gameID  pgn       
## [103,] "beta2" "7...Nc6" 
## [104,] "beta2" "8.a3"    
## [105,] "beta2" "8...Nf6" 
## [106,] "beta2" "9.Nc3"   
## [107,] "beta2" "9...Bf5" 
## [108,] "beta2" "10.O-O-O"
```

It avoids ambiguity between white and black moves by giving white moves a single dot, ".", and black moves three dots, "...".
