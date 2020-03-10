# Technical Setup

If you haven't already, familiarise yourself with our [architecture](../develop/architecture.md)

You will need to setup atleast one game server, and the tournament server. We suggest you get this setup way 
in advance so that you can identify any potential server and inter-server connection issues.

## Game Server(s)

We have the following official game server projects available for you to use, please see their READMEs for information on 
how to depoy them.

| Game | GitHub Project | License |
|------|----------------|---------|
| Ultimate Tic Tac Toe | https://github.com/socialgorithm/ultimate-ttt-game-server | MIT |
| Tic Tac Toe | https://github.com/socialgorithm/tic-tac-toe-game-server |  AGPL-3.0 |

## Tournament Server

Run the following command to start the tournament server:

```
npx @socialgorithm/tournament-server --port 8000 --game <game-server-address>
``` 

See [the GitHub project for more information](https://github.com/socialgorithm/tournament-server/)

## Connectivity Options

Participants/their player code will need to be able to connect to both the Tournament Server and Game Server via Websocket connections.
