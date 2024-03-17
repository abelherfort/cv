## Compass

 A Minecraft network-level arena management system, that manages worlds in an Object Storage. It can load dynamically unique and ephemeral world sessions to game servers, manages player connections.

This system made it so, the all world and arena loading logic could be standardized and be done with just few lines of code.

The compass agent would run on all lobby and game servers, and would dynamically register and unregistered themselves whenever needed. 

Whenever requesting a session, the agent would search for an available game server instance, that matched the requirements, send a world load bootstrap request, and after completion, send the players to the desired game server.

### Infrastructure

![architecture](https://media.yoursit.ee/cv/compass/architecture.png)
### Session loading

The lobby server would keep track of the loading process, therefore all stages and errors could be handled. The unique and template worlds are loaded from an object storage.

![bootstrap-lobby](https://media.yoursit.ee/cv/compass/bootstrap-lobby.png)

![bootstrap-game](https://media.yoursit.ee/cv/compass/bootstrap-game.png)

Unique worlds are periodically synchronized with the object storage, so if a later returns to the world, they can continue right at where they left.

![unique-world](https://media.yoursit.ee/cv/compass/unique-world.png)

### Session unloading

After all players disconnecting from the game server of the session, a timeout would start. If a player would rejoin during the timeout, the session would recover and turn to active state. This allows us to minimize load on the network, say if the player quickly connected to another server for some reason; we do not have to load the world again.

![session-unload](https://media.yoursit.ee/cv/compass/session-unload.png)
