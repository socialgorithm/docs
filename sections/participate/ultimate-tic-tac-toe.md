---
showToc: true
---

# About

![Ultimate Tic Tac Toe board, with an animation for some rounds](/assets/uttt.gif)

This is the board for an **Ultimate Tic Tac Toe** game, it's essentially a collection of nine small *regular* Tic Tac Toe games.

The first player can play in any cell of any of the small boards. The coordinates of the **move in the small board** determine which *board* the next player has to use to play.

On each turn, the valid small board is **highlighted in yellow**. Each player's move is displayed in *blue/red*.

You'll be playing on the big board, but in order to *"win"* each cell, you have to win the **game within that cell**.

# Rules

1. You only play on the small boards.
1. The first player can play on any cell of any small board.
1. You must play on the small board that corresponds to the cell the other player played at.
1. If you are *sent* to a board that has been won already, you must play on any other board. *(Some people play with variations of this rule, but we believe this makes for the most interesting algorithms)*
1. To win the game you must have 3 in a row in the big board in any direction.

## Example

If this is the first move of the game:

![Example of a first move](/assets/3-first-move.jpg)

Then the other player has to play on the top right board:

![Board where the next player has to play in](/assets/4-second-move.jpg)

The game may seem simple at first, but the fact that you get to decide where your opponent plays next means that you'll have to look ahead several turns to decide what the best move is.

You should start by playing **at least once on paper** with a friend, to get an idea of how the game goes. Sometimes giving up one of the smaller games is necessary to win the big one!

# Writing a Player

We're going to write an algorithm that can play UTTT, exciting right? :)

At the most basic level, a player needs to be able to calculate a **valid move**, and receive **opponent moves**. Every time it receives a move from its opponent it will run some calculations, and return what it considers to be the optimal move.

A simple start would be to have a program that does just that:

```js
// pseudo-code example of the most basic methods
addOpponentMove(board, move) {
    // store his move
}

addMove(board, move) {
    // store our move
}

getMove() {
    // calculate a new move
    return {
        board: ...,
        move: ...
    };
}
```

## Starters

Starter packs provide a basic implementation for that play at random, so you can focus on improving the logic that picks the moves.

In a terminal window, navigate to the folder where you want to store this project (`cd <folder-name>`), and run in the language of your choice:

> If you have a Github account: Fork the project and clone it locally, so you can share your amazing implementation with the world!

### JavaScript

```console
git clone https://github.com/socialgorithm/ultimate-ttt-player-js.git
cd ultimate-ttt-player-js
npm install # install dependencies
```

### Python

```console
git clone https://github.com/socialgorithm/ultimate-ttt-py.git
cd ultimate-ttt-py
```

## Run the Random player

The starter project comes with a player that plays moves at random. You can ensure everything works as it
should by running this player against the `uabc` random player:

### JavaScript

Inside the `src` folder you'll find three implementations:

* `defensive/logic.js` - is a good start, as it already provides some minimal logic to compete.
* `firstAvailable/logic.js` - selects the first available valid move, whatever that is.
* `random/logic.juabc@latest -p -f "python3 run_player.py"s` - selects any valid move at random.

`@socialgorithm/uabc@latest -p -f "python3 run_player.py"`

### Python

The `player.js` file does the stdin/stdout work, and you shouldn't edit it. It requires the file `src/defensive/logic.js`, which is the one you could start with.

It's interesting to look at each of these to see how they implement the logic and learn about it before starting to make changes.

## Improve the player

### Python

You can view the code that does this by 
opening the `players/random.py` file. The code will be something like:

```python
class Random(StdOutPlayer):
    def __init__(self):
        super().__init__()

    def get_my_move(self) -> Tuple[MainBoardCoords, SubBoardCoords]:
        main_board_coords = self.pick_next_main_board_coords()
        sub_board = self.main_board.get_sub_board(main_board_coords)
        sub_board_coords = self.pick_random_sub_board_coords(sub_board)
        return main_board_coords, sub_board_coords

    def pick_next_main_board_coords(self) -> MainBoardCoords:
        if self.main_board.sub_board_next_player_must_play is None:
            return random.choice(self.main_board.get_playable_coords)
        else:
            return self.main_board.sub_board_next_player_must_play

    @staticmethod
    def pick_random_sub_board_coords(sub_board: SubBoard) -> SubBoardCoords:
        return random.choice(sub_board.get_playable_coords())
```

As you can see, the `get_my_move` method is the one you need to edit, it returns a tuple of `MainBoardCoords` and 
`SubBoardCoords` (which are essentially the same thing, they contain a `row` and a `column`).

To keep things simple, start off with editing the `players/random.py` file.

##### Other players
There are two other players included in the code: FirstAvailable and Defensive. You can pass their names as a command line parameter to `run_player.py` to use them. For example:
`uabc -p -f "python3 run_player.py Defensive"`.

The Defensive player has code to check for winnable positions, which you might find useful when implementing your own player.

The relevant functions are:
* `get_my_move`: first it tries to find a winning or defensive position in all the boards that are legal to play, if there is none, it works like FirstAvailable (this logic is similar to Random but it picks the first item from the list of valid sub-boards and positions instead of using `random.choice`.
* `get_move_for_board`: finds winning and defensive moves in a single sub-board.
* `get_closeable_positions`: finds winning moves for a specified player. get_move_for_board uses this for itself and the enemy to find winning and defensive moves respectively. The function works by checking for winning moves in the three rows, the three columns and the two diagonals, then filtering out those that have no winning move.
* `_column`, `_columns`, `_major_diagonal`, `_minor_diagonal`: these return a single column, all the columns, and the two diagonals from a sub-board. get_closeable_positions uses these as helper functions.
* `get_winning_position`: finds a winning position on a single line. If the specified player has one less fields filled in than the length of the line, the remaining field is the winning move as long as it is empty. In any other case there is no winning move.

#### Game Engine

There is a game engine provided that keeps track of the state of the game and does a lot of the heavy lifting
for you. This can be accessed through the `self.main_board` object, and you can consult
the [API Reference](https://ultimate-ttt-py.readthedocs.io/en/latest/) for all the available methods 

#### Sources

Some folks prefer to view the source of the game engine directly rather than using the API reference. You can
find all the sources in the `engine/` directory.

## Continue: [Analyse Your Games](./analyse-games.md)

--------

## Troubleshooting

#### Can't find the project!

After running `git clone` without errors you should have the project in the folder the terminal is in. To find out where this is type `pwd` (or `echo %cd%` on Windows).

> We have prepared [some ideas](./ideas.md) on how to write the AI for your player that may help you out!

## Continue: [Running Locally](./analyse-games.md)
