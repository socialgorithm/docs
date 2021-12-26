---
showToc: true
---

# Writing A Game

These are the parts involved in writing a game/challenge:

* Write the **Game Logic**
* Connect the Game Logic to an existing **Game Server Library** / Roll your own
* Write a **Sample Player**
* Connect the Tournament Server/Players to the Game Server to test
* Write the **Game UI**

## Writing the Game Logic

You can write the game logic in any language you prefer, but it may be quicker for you to write in a language that is already supported by us (see the table below). We provide Game Server Libraries that setup a socket server and provide entrypoints for your game logic. These libraries integrate with the rest of the Socialgorithm stack, allowing you to abstract communication logic and focus on writing your game logic/engine.

You should strive to have unit/end-to-end tests for your game logic.

## Game Server Libraries

### Existing Game Server Libraries

Please see the repositories for information on how to integrate your games:

| Language | Repository | Example |
|----------|------------|---------|
| JavaScript / TypeScript | https://github.com/socialgorithm/game-server-js | https://github.com/socialgorithm/tic-tac-toe |
| Java / JVM | https://github.com/socialgorithm/game-server-java | Coming Soon |

We are open to contributions in other languages, please see below on how to write your own Game Server library. 

### Roll your own

The best way to do this is to port an existing one, so pick one from the table above and go to town!

If the server libraries do not meet your expectations, you can always roll your own. To communicate with the SG Tournament Server/other games consumers, a Game Server must send the socket events expected by the Tournament Server and execute functionality based on the events sent by the Tournament Server. This is described below:

| Event | Required? | Description | Format |
| ----- | --------- | ----------- | ------ |
| `GAME_INFO` | Y | On every new connection to the Game Server, it must emit a `GAME_INFO` event so consumers know the type of the game server | |
| `START_GAME` | Y | The Tournament Server sends this when the game is starting, the Game Server should initialize a game. Any future communication on this connection is regarding this game only | |
| `GAME__PLAYER` | N | * The Tournament Server sends this when a player has sent a message to the game <br>* The Game Server can send this to communicate with a player | |
| `GAME_UPDATED` | N |  The Game Server can send this when it wants to communicate game updates to spectactors | |
| `GAME_ENDED` | Y | The Game Server must send this when the game has ended. The Tournament Server will then close the game connection. | | 

## Writing a Sample Player

Writing a sample player will not only let you test your game logic, but will later serve as a starting point for participants in your competition. Again, you should have independent tests of your player to ensure it works as expected before integrating it.

We provide **UABC** (Ultimate Algorithm Battle Client), a command-line application that abstracts communication over the network by connecting to the specified Tournament Server, executing your player file, and acting as a bridge between the STDIN/STDOUT of the file and the websocket port of the Tournament Server. In practice, this means that your player only needs to listen for data/moves on STDIN and output data/moves on STDOUT.

See the [UABC Repository](https://github.com/socialgorithm/uabc) for instructions on how to install/use it with your sample player.

## Test with the Tournament Server and Web UI

The Tournament Server helps to proxy messages between players and game servers, and once you have tested your game logic to ensure it works, you can start to test against sample players (over the network).

To install the Tournament Server, check out its [repository and README](https://github.com/socialgorithm/tournament-server/). Follow the instructions to install it and connect it to your game server.

You can then use our [Web UI](https://github.com/socialgorithm/tournaments.socialgorithm.org) to start matches between your sample players to test that the entire game works as expected.

## Game UI

While we provide a UI to display Tournaments and their statistics, each game can have its own UI that will render statistics or game boards (or anything really). To write the game UI, you will need to provide a ReactJS component that will accept game statistics and render accordingly (e.g. receive player moves and render a game board). 

The format of the game statistics is left up to your game and its renderer. Your game, when connected to the Tournament Server, will emit `GAME_ENDED` messages, and optionally `GAME_UPDATED` messages. The tournament server will pass these messages on to spectators, including the Web UI, which will contain your React component for rendering the game board.

So, to get started with writing the Game UI, follow the instructions on the [Web UI repository](https://github.com/socialgorithm/tournaments.socialgorithm.org) to obtain the source code and to read on how to add your UI.
