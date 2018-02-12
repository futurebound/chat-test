# Lab 6 - TCP Chat Server

**Author**: Mitchell
**Version**: 1.0.0

## Overview
In this lab we were tasked to created a TCP chatroom. Clients should be able to connect using a netcat or telnet client, give themselves nicknames to be referred to as and directly messaged as by other users, and be able to talk to each other. There should be special commands available to users such as quit, list all users, set/reset their nickname, and send direct messages to other users by their ID/nickname.

## Getting Started
To get this application up and running, fork and/or clone this repository using the `git clone <git repository link>` command in your terminal. Next, run the `npm install` command, which will install all the necessary dependencies in the accompanying package.json file. You can open up the code in your favorite editor to explore/modify the code, see how the tests are structured, and create tests of your own if desired.

If exploring the functionality of the chat server, you can enter the terminal command `npm start` to initiate a server listening on port 3000. If that port is occupied, you can add your own desired port to a `.env` file in the lab-mitchell/ directory such as `PORT = <desired port number>` in said file. You can then open new terminal tabs or terminal instances and enter `nc localhost 3000` or `nc localhost <desired port number>` to connect to the server. Each new tab and `nc localhost <desired port number>` will create a new user with a unique ID to the chat pool, and each time a new user enters the chat all users currently logged in will be broadcast a message informing them of that new user connection. With multiple terminal tabs/instances open, you can enter messages in the respective tabs which will be sent to and visible in all other instances.
**NOTE** _[NC - NetCat for use with current Macs, if using TelNet, enter the command `telnet localhost 3000` instead]_

## Description
There are three main files in the project: the entry point server.js, cmd.js in the lib/ directory, and client.js in the model/ directory.

Client.js is home to a client constructor, which is an exported function expecting a single socket argument, and has ID, nickname, and socket properties.

Cmd.js exports a function expecting two arguments, data and connected (users). Its purpose is to house possible custom commands that can be entered by a user once connected to the server. Those commands are recognized by using the `@` character before the command, and are as follows:
* `@quit` ~ Disconnects user from chat/server, and informs channel members that the user has left.
* `list` ~ Displays list of all currently connected users to member who entered command.
* `@nickname <new-name>` ~ Changes nickname of user who enters command to specified name. **NOTE** Only accepts single word nicknames, nicknames with spaces will return and error stating this.
* `@dm <target-user/nickname> <message>` ~ Directly messages the targeted user. Only the targeted user and the sender can view these messages. If the targeted user does not exist, command will return an error stating that.

Any misspelled command containing the `@` character at the beginning of the line, or any command that is not registered will return an error alerting the user that the command they attempted to use does not exist.

## Credits/Collaborators
[Daniel Logerstedt](https://github.com/daniellogerstedt) ~ https://github.com/daniellogerstedt
Pair programmed cmd.js, lines 24 - 38 of said file.

[Node.js Net Module Documentation](https://nodejs.org/api/net.html) ~ https://nodejs.org/api/net.html
[NPM UUID Package Documentation](https://www.npmjs.com/package/uuid) ~ https://www.npmjs.com/package/uuid
[NetCat Wiki](https://en.wikipedia.org/wiki/Netcat) ~ https://en.wikipedia.org/wiki/Netcat
[TelNet Wiki](https://en.wikipedia.org/wiki/Telnet) ~ https://en.wikipedia.org/wiki/Telnet