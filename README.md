# EncryptedChat

This repository contains a Java internet group chat application that demonstrates the [Diffie-Hellman key exchange](https://en.wikipedia.org/wiki/Diffie–Hellman_key_exchange). It consists of a server to which multiple clients can connect via sockets.

![](/assets/header.png)

## Getting started

**1. Server** Open and run `ChatServer.java`. This will create a server listening to local clients on port `1111`. You may change the port to one that suits you better.

**2. Clients** Open `EncryptedChat.java`. Three sample clients are preconfigured. Add/remove clients and edit the usernames as needed. In case you've adjusted the server port, do so as well in each client initializer. Run the file to start chatting locally between clients. To add further independent clients, configure them in `EncryptedChat.java` as well and run the file in a new process.

**Cleanup** Sent messages are permanently stored so they don't get lost upon terminating the server or its clients. When those messages are no longer needed, you may delete `~/EncryptedChatMessages_server.ser` and `~/EncryptedChatMessages_[chat client username].ser`.

### Internet chat

To allow communication between clients that are not necessarily located in the same local network, additional setup is required:

1. Open the router settings of the network in which the chat server is running and locate the public IP address (e.g. `xxx.xxx.xxx.xxx`).
2. Replace `localhost` in the chat client initializer with that IP address:
```java
new ChatClient("Alice", "xxx.xxx.xxx.xxx", 1111);
```
3. Forward port `1111` to internal port `1111` of the servers local IP. You may assign a static IP to the server.

## :warning: Security

This app was created as part of a school presentation and is for demonstration purposes only! Notably the values chosen for `g` and `p` are not secure and not suitable for real-world applications – those values must be carefully selected and usually reside in the 1024 to 4096 bit length range. Furthermore, opening and forwarding ports may introduce new attack vectors.
