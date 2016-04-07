---
title: Introduction to ChessDoodle Functions
date: 2016-03-30 06:50:08
author: Josh Merrell
comments: false
tags:
- BankerDoodle
- R Packages
- Analytics
- Chess
categories:
- R Packages
---

This workspace is geared to help the user to explore and think about the chessboard. It is available [here](https://github.com/brantmerrell/chessdoodles/blob/master/chessDoodles.RData):

```{r}
# clear workspace
rm(list=ls())

# load workspace
load("chessDoodles.RData")
```

The regex patterns interpret strings. 

```{r}
ls(pattern = "Pattern")
```

The pathPrior() function is named after the term *a priori*. For a given input piece and square of the chessboard, it returns the *path* the piece can take on an empty chessboard, *prior* to the circumstance that arise when a game is in play.

```{r}
pathPrior(piece = "bishop", square = "e5")
pathPrior(piece = "knight", square = "e5")
```

The pawn is the only piece unable to move backwards, and its *direction* depends on its color.

<!-- More -->

```{r}
pathPrior(piece = "black pawn", square = "e5")
pathPrior(piece = "white pawn", square = "e5")
```

It is the only piece whose color needs to be specified for pathPrior.() to work effectively. *Post.()* functions are conversely named after the term *a posteriori*. They trim each piece's options according to the circumstances of the entire board. 

```{r}
ls(pattern = "Post")
```

They cannot be used unless a snapshot of the chessboard's position exists for them to analyze. The snapshots exist as rows of the *position* data frame, which has one variable for each square of the chessboard. Each variable in *position* is a square of the chessboard,

```{r}
colnames(position)
```

and each observation is a snapshot of the game:

```{r}
set.seed(123); 
position[sample(2:nrow(position),1), 
         sample(1:ncol(position),10)]
```

The first row is the *empty* chessboard, with no pieces listed for any of the squares. The second row is the *zero* position, with pieces set at starting positions.  

We can compare the mobility of a white knight on b1 before and after the pieces are set up:

```{r}
pathPrior(piece = "knight", square = "b1")
pathPost.(square = "b1", game_pgn = "000_zero")
```

Because of the game_pgn input, *pathPost.* knows that the piece on h2 is a white knight, and that it cannot move to **d2** because that space is occupied by another pawn.

Let us begin by observing the [game](https://www.chess.com/echess/game?id=131764454) I am currently playing. We can modify the link into the format *"http://username:password@chess.com/..."* and pass it to the *rawToTidy()* function as follows:

```{r}
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
games <- rawToTidy(Link)
print(games)
```

Now we can expand this pgn from a single string to a data frame of moves using *tidyToPgn()*.

```{r}
moves <- as.data.frame(tidyToPgn(games,n=1, string = "xmpl"))
print(moves)
```

The first move is pawn to e4. Inputing it into the *newPosition()* function replicates the last (or specified) row of the *position* frame, places the white pawn on e4, and removes it from e2.

```{r}
position[,c("e2","e4")]
newPosition(new_pgn = "1.e4", 
            startPosition = nrow(position))[,
                                            c("e2","e4")]
```

newPosition() is designed to sequentially build on the *position* object. 

```{r}
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

These functions will provide the analytic muscle for future blogging analyses. 