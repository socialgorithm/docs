# Tic Tac Toe: Writing a Player

You will now write an algorithm (player) that can play Tic Tac Toe!

Your player needs to:

1. Play a valid move.
1. Receive an opponent's move (and respond with another valid move).

> Now is a good time to ensure you have the `tic-tac-toe-starter` repository available (see [The Welcome Page](../participate.md)), and open it in your code editor.

## The Random Player

The starter pack provides a player that plays Tic Tac Toe by picking valid moves at random. Not the best strategy. You will soon improve it, but let's ensure the random player works on your machine first.

### Running the Random Player

Run the following command in the `tic-tac-toe-starter` directory to install required dependencies:

```
npm install
```

Now run the following command to test that the player runs:

```
uabc -p -f "node run_player.js"
```

If all goes well, you should see a game summary. Our algorithm client utility (`uabc`) has run the random player against itself.

### Improving the Random Player

So now you've got the random player working, let's improve it!

In the starter directory, find the `players/random.js` file. This file contains the code for the random player, and **is the file you will need to edit**. It is loaded and run by the `run_player.js` file you used earlier.

To improve the random player, you will need to edit two functions:

1. LINE XX: `onFirstMoveRequest: () => Move`  
Function that takes no arguments and returns a move
1. LINE XX: `onOpponentMove: (move: Move) => Move`  
Function that takes the opponents move and returns a move

Where `Move` is an object with `row` and `col` co-ordinates starting from `0`, i.e.:

```js
Move = {
  row: [0 to 2],
  col: [0 to 2]
}
```

Carefully read the two functions so you understand what they are doing, make your changes, and re-connect your player to your test tournament.

When you are ready to compete, go ahead and connect your player to the real tournament.

We have provided some [ideas](./ideas.md) that can guide your changes, should you need guidance.