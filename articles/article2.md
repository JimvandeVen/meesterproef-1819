# Socket.io

## Introduction

A couple of weeks ago I worked with socket.io for the first time. Socket.io lets you create, for example, a chat application that is easy to implement. Providing a two-way communication channel between a client and a server. This means the server can push messages to clients. Whenever you write a chat message, the idea is that the server will get it and push it to all other connected clients.

![Socket](temp/socket.jpg)

## Table of Contents
- [What is socket.io](#what-is-socket)
- [How to begin](#how-to-begin)
- [Rooms and Namespaces](#rooms-and-namespaces)
- [Different emits](#different-emits)
- [Coupling with an API](#coupling-with-an-api)
- [What we have learned](#waht-we-have-learned)
- [Sources](#sources)

## What is socket

Socket.IO is a library that enables real-time, two-way communication between the browser and the server. This works much in the way of eventlistners in Javascript. The two communicating parties are a Node.js server and a Javascript client library. 

Each client that connects to the server will get a socket. This unique socket then can communicate with the other sockets through the server. I will explain how this works later on.

The main features of socket.io are:

- reliability (it works even with firewalls and antivirus software)
- Auto-reconnection support (unless otherwise instructed the client will try to reconnect with the server forever)
- Disconnection detection (both the server and the client know when the other one is not responding)
- Room support (This is a useful feature to send notifications to a group of users)

## How to begin

First you setup a simple HTML webpage that serves out a form and a list of messages. We do this with a Node.js framework using an express server.

Server:
```js
const express = require('express');
const app = express();
const http = require('http').Server(app);
const io = require('socket.io')(http);

app.get('/', index)


function index(req, res) {
    res.render("pages/index");
};

http.listen(process.env.PORT || 3000)
```

HTML:
```html
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m"/><button>Send</button>
    </form>
  </body>
</html>
```

Now that we have a srever and a html page that has a form in it we want to create a connection between the client and the server. For this we create a client.js file that contains:

```js
const form = document.querySelector('.message');
const inputValue = document.querySelector('#m');
const messages = document.querySelector('#messages');

form.addEventListener("submit", function(e) {
  e.preventDefault();

  socket.emit('chat message', inputValue.value);
  inputValue.value = "";
  return false;
});
```

With the `socket.emit`, that works much like an event handler you can 'emit' an event and send data to the server. In this case we send the value of the input field. The 'eventlistener' on the server looks like this:

```js
io.on('connection', function(socket) {
  socket.on('chat message', function(msg) {
    io.emit('chat message', {msg: msg);
    });
});
```

What you also see in the piece of code above is something new, `io.emit('chat message', {msg: msg);`. This line emits the message again, but also to all the other clients. For the clients to receive this message there needs to be another listener on the client side:

```js
socket.on('chat message', function(msg){
      messages.innerHTML +=`<li>${msg}</li>`
});
```

And here you have it! The most simple, but still awesome, version of a chat. That wasn't so hard I think so lets take it up a notch.

## Rooms and Namespaces

Socket.io allows you to 'namespace' your sockets. This means that those sockets use different endpoints and thus separating communication channels. Those namespaces are really easy to implement.

On the server you specify the namespace by calling the `of` function like so:

```js
const nsp = io.of('/my-namespace');
nsp.on('connection', function(socket){
  console.log('someone connected');
});
nsp.emit('hi', 'everyone!');
```

On the client side you tell the socket to connect to that namespace like so:

```js
const socket = io('/my-namespace');
```

## Different emits

## Coupling with an API

## What we have learned

## Sources
