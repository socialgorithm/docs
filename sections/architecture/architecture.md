# Architecture

![Socialgorithm Architecture](architecture.png)

# Writing Games

You can either use a Socialgorithm provided Game Server Library, or write your own that conforms to our interface and that the Tournament Server will talk to.

All game servers conform to the following interface, providing the ability to send updates on game progress to players or the tournament server

```
interface GameServer {
    bindings: GameServerBindings,
    sendPlayerMessage: (player: string, payload: any) => void;
    sendGameMessage: (type: MessageType, payload: any) => void;
}
```

All games must implement game server bindings, listening to events from the Tournament Server/Game Server

```
interface GameServerBindings {
    startGame: (options: GameOptions) => void;
    onPlayerMessage: (player: Player, payload: any) => void;
}
```

## JavaScript

See [JavaScript Game Server Library](https://github.com/socialgorithm/game-server-js)

## Java/JVM languages

Coming soon!

## Other languages

Coming soon!