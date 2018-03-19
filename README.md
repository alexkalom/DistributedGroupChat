# DistributedGroupChat

# Disclaimer
This is the result of an assignment given during the distributed systems course at ece ntua.

# Description
This repository contains a distributed group messenger (irc style), that can send messages to a group of clients in a distributed manner. There is central tracker whose only purpose is to keep track of the clients (username, IPs, ports, etc.). Each client registers with the tracker, and though the tracker learn about other clients in the same groups as him. Clients talk to each other using udp, and uses two different protocols, to ensure fifo order of the messages, or fifo + total ordering. For total ordering we implemented the ISIS algorithm.


# Installation
The installation process of this distributed group messenger is fairly simple. Just clone this repository and build the source using ant.
```
$ cd /path/to/repository/
$ ant
```

If your jdk_home directory isn't the /usr, you should first set your jdk_home directory by editing the build.properties file.

# Starting the tracker

In order for the messenger to work, there has to be a live tracker. To start the tracker do

```
$ cd /path/to/repository/out/production/DistributedGroupChat
$ java -cp ".:lib/guava-19.0.jar" tracker.Tracker
```

Now to start a client
```
$ cd /path/to/repository/out/production/DistributedGroupChat
$ java client.Client debug=false tracker=147.102.201.123:3000 protocol=isis
```

where tracker is the address of the tracker and protoco is the protocol that the clients follow for message delivery (isis for total order and fifo, fifo for fifo).

When a client has started it needs to register with the tracker. To do that, simply type "!r", at the prompt. Then to join a group type "!j groupname" after that, you can type messages and other clients in the same group, will see your messages.