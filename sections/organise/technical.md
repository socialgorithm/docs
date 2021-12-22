# Technical Setup

If you haven't already, familiarise yourself with our [architecture](../develop/architecture.md)

You will need to setup atleast one game server, and the tournament server. We suggest you get this setup way 
in advance so that you can identify any potential server and inter-server connection issues.

## Game Server(s)

We have the following official game server projects available for you to use, please see their READMEs for information on 
how to deploy them.

| Game | GitHub Project | License |
|------|----------------|---------|
| Battleships | https://github.com/morganstanley/battleships | AGPL-3.0 |
| Tic Tac Toe | https://github.com/socialgorithm/tic-tac-toe | AGPL-3.0 |
| Ultimate Tic Tac Toe | https://github.com/socialgorithm/ultimate-ttt | MIT |

## Tournament Server

Run the following command to start the tournament server:

```
npx @socialgorithm/tournament-server --port 8000 --game <game-server-address>
``` 

See [the source repository for more information](https://github.com/socialgorithm/tournament/)

## Connectivity Options

Participants/their player code will need to be able to connect to both the Tournament Server and Game Server via Websocket (Socket.IO) connections.
