# Architecture

Coding challenges/games in Socialgorithm consist of:

* Players: Code/logic written by competition participants to compete against others (e.g. a Battleships player)
* Game Engine/Server: Runs games between players, processing moves/actions from Players, ensuring consistency and signalling game updates/end.
* Tournament Server: Matches up players, communicates with the game server to start games or read results, and ranks players in the tournament leaderboard. 

All communication occurs over Websockets. Socialgorithm provides a number of libraries that abstract Websocket client/server setup and communication, so that competition players can focus on writing the best algorithms, and game writers can focus on writing fun games.

This architecture diagram shows how each piece integrates together:

![Socialgorithm Architecture](architecture.png)

# Games and Players

If you are interested in hosting a competition, you can either use one of our existing games, or integrate your own. See our[available games](https://socialgorithm.org/workshops/) or the documentation for how to [write your own game](/sections/games/writing-games.md).