# Architecture

![Socialgorithm Architecture](architecture.png)

The Socialgorithm platform is made up of:

* Players: Code/AI written by competition participants to compete against others (e.g. a Battleships player)
* [Web UI](https://tournaments.socialgorithm.org/): Interface that allows competition participants/admins to view/control player matching and game options. 
* [Games](./write-a-game.md): Servers that run games, processing moves/actions from Players, ensuring consistency and signalling game updates/end.
* [Tournament Server](https://github.com/socialgorithm/tournament/packages/server): Server that communicates with multiple Game Servers to start games or read results, and rank players in a tournament leaderboard.

All communication occurs over Websockets. 

Socialgorithm provides a number of libraries that abstract Websocket client/server setup and communication, so that competition players can focus on writing the best algorithms, and game writers can focus on writing fun games.