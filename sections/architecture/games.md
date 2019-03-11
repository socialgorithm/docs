# Writing Games

We provide Game Server Libraries that setup a socket server and provide entrypoints for your game logic. These libraries integrate with the rest of the Socialgorithm stack, and allow you to abstract communication logic and focus on writing your game logic/engine.

## Available Game Server Libraries

Please see the repositories for information on how to integrate your games:

| Language | Repository | Example |
|----------|------------|---------|
| JavaScript / TypeScript | https://github.com/socialgorithm/game-server-js | https://github.com/socialgorithm/tic-tac-toe |
| Java / JVM | https://github.com/socialgorithm/game-server-java | Coming Soon |

We are open to contributions on other languages, please see below on how to write your own Game Server library.

## Roll your own

If the server libraries do not meet your expectations, you can always roll your own. To communicate with the SG Tournament Server/other games consumers, a Game Server must send the socket events expected by the Tournament Server and execute functionality based on the events sent by the Tournament Server. This is described below:

| Event | Required? | Description | Format |
| ----- | --------- | ----------- | ------ |
| `GAME_INFO` | Y | On every new connection to the Game Server, it must emit a `GAME_INFO` event so consumers know the type of the game server | |
| `START_GAME` | Y | The Tournament Server sends this when the game is starting, the Game Server should initialize a game. Any future communication on this connection is regarding this game only | |
| `GAME__PLAYER` | N | * The Tournament Server sends this when a player has sent a message to the game <br>* The Game Server can send this to communicate with a player | |
| `GAME_UPDATED` | N |  The Game Server can send this when it wants to communicate game updates to spectactors | |
| `GAME_ENDED` | Y | The Game Server must send this when the game has ended. The Tournament Server will then close the game connection. | | 