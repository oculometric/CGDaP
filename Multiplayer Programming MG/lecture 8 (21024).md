object replication - transmitting/synchronising an object's state from one client to another
need to identify the packet as an object replication packet, need to uniquely identify the object, and indicate the class of object.

with a JSON packet, we can just make a different packet class and serialise it, serialising with it the information about what type of packet it is and what type of object it is talking about.

if the game world is small enough we can do Naive World State Replication (i.e. just send the info for the entire world over as a single packet).

however, it's usually more efficient to only transmit what is required (i.e. what has changed). could be done with a dirty-flag protocol.

balance perfectness of syncing with optimal code (not transmitting the entire world every single frame).

sometimes we don't want to just transmit states, but function calls. remote procedure calls can do this. this is done by just having a packet marked appropriately, with space for the parameters for the function call (this will need to be handled appropriately on the client).

`Action`s in C# are pre-made delegates which you could use to handle events which can be broadcast across clients.