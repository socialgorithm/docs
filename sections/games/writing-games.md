# Writing Games

We provide Game Server Libraries that setup a socket server and provide entrypoints for your game logic. These libraries integrate with the rest of the Socialgorithm stack, and allow you to abstract communication logic and focus on writing your game logic/engine.

## Available Game Server Libraries

Please see the repositories for information on how to integrate your games:

| Language | Repository | Example |
|----------|------------|---------|
| JavaScript / TypeScript | http://github.com/socialgorithm/game-server-js | https://github.com/socialgorithm/tic-tac-toe |
| Java | Coming Soon | |
| Python | Coming Soon | |

## Roll your own

If the server libraries do not meet your expectations, you can always roll your own. To communicate with the SG Tournament Server, you need to ensure that it reacts accordingly to the following socket messages:

Input from Tournament Server (implement/react to these):

* `startGame`: This event is sent to initialize the game
* `playerMessage`: This event is sent when a player has sent a message (e.g. made a move)

Output to Tournament Server (call these at appropriate times):

* `playerMessage`: Use this event to communicate directly with players (e.g. to report an opponent move/ask for a move)
* `gameMessage`: Use this event to broadcast game state (e.g. stats update/game end)
