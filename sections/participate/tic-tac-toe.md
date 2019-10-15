---
showToc: true
---

# About

![Tic Tac Toe Animation](./tic-tac-toe.gif)

We've all probably played a game of Tic Tac Toe / Noughts and Crosses, this classic game is quite simple to play, but it is an interesting challenge to write an algorithm that can play (intelligently) for you.

# Rules

1. You play on a 3x3 game board.
1. You and your opponent will play one after another.
1. You need to get 3 cells in a row, in any direction, to win.
1. If you take too long to play (usually 100ms), you lose.

# Writing Your Own Player

You will now write an algorithm (player) that can play Tic Tac Toe!

Your player needs to:

1. Play a valid move.
1. Receive and record an opponent's move.

> Now is a good time to ensure you have the `tic-tac-toe-player` repository available (see [The Welcome Page](../README.md)), and open it in your code editor.

# The Starter Player

The starter pack provides a player that plays Tic Tac Toe by picking valid moves at random. Not the best strategy. You will soon improve it, but let's ensure the starter player works on your machine first.

## Running the Starter Player

Run the following command in the `tic-tac-toe-player` directory to install required dependencies:

```
npm install
```

Now run `uabc` to connect your player to the lobby you created earlier (replacing `YOUR_LOBBY_NAME` and `YOUR_PLAYER_NAME` with appropriate values):

```
uabc --host "https://sg-tournament.herokuapp.com" --lobby "{YOUR_LOBBY_NAME}" --token "{YOUR_PLAYER_NAME}" -f "node run_player.js myPlayer"
```

If all goes well, your player should show up in the list of available players. 

You now need another player to compete against. Open a new terminal window and run the above command again (changing the player name). 

You can now start the game (you may have to click "Play Next Match" in the top right corner).

## Improving the Starter Player

So now you've got the starter player working, let's improve it! In the starter pack, find the `players` directory. 

So far, you have been running the `myPlayer.js` implementation. This is a copy of the `random.js` file, so as you improve `myPlayer`, you can ensure you are getting better results versus `random`.

Let's dig into the `myPlayer.js` file to see what it is actually doing. There are three functions of interest to us:

1. LINE 17: `init: () => void`
Function that is called when a new game is about to begin (the player will normally reset their board state at this time).
1. LINE 21: `getMove: () => Move`  
Function that is called every time it is your move.
1. LINE 28: `onOpponentMove: (move: Move) => Move`  
Function that is called every time the opponent makes a move.

If you read the `getMove` function, you will see that it calls the `getRandomValidMove()` function. As the name of the function indicates, this function returns a random valid move, which is then returned to the server.

So, to stop playing randomly, replace the call to the `getRandomValidMove()` function with a function of your own. It might help you to first understand what that function is doing, copy it and then make your modifications. You can also refer to the [SubBoard API](https://socialgorithm.org/ultimate-ttt-js/classes/_subboard_.subboard.html) to see what functions are available on the `SubBoard`/`game` object.

Every time you use the `addMyMove` or `addOpponentMove` functions, remember that the board object is copied, so (as is done in the `getMyMove` function), you must update the existing `game` variable with the return value of `addMyMove`/`addOpponentMove`, i.e.:

```js
this.game = this.game.addMyMove(myMove);
```

## Testing your improvements

To test your improvements, run the `myPlayer` implementation (or any other player you have created), against the `random` implementation. You can connect the random implementation to your lobby by running:

```
uabc --host "https://sg-tournament.herokuapp.com" --lobby "{YOUR_LOBBY_NAME}" --token "random" -f "node run_player.js random"
```

## Competing

To compete, simply replace the name of your test lobby with the lobby name given to you by the Socialgorithm mentors running the workshop.

***Good luck!***