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

Socket.IO is a library that enables real-time, two-way communication between the browser and the server. This works much in the way of event listeners in Javascript. The two communicating parties are a Node.js server and a Javascript client library. 

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

Now that we have a server and a html page that has a form in it we want to create a connection between the client and the server. For this we create a client.js file that contains:

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

With the `socket.emit`, that works much like an event handler you can 'emit' an event and send data to the server. In this case we send the value of the input field. The 'event listener' on the server looks like this:

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

And here you have it! The most simple, but still awesome, version of a chat. That wasn't so hard I think so let’s take it up a notch.

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

Within each namespace you can also let the sockets `join` or `leave` rooms. This especially useful when you want to create different channels to which the client can subscribe. Think about different channels in slack, or different group chats in WhatsApp.

Rooms are, agin, really easy to implement. In the client side you can send an emit like so:

```js
socket.emit('joinPro')
```

Then on the server you listen for this event:

```js
io.on('joinPro', function(socket){
  socket.join('pro');
});
```

To send messages to these specific rooms you use `to` or `in` when broadcasting or emitting:

```js
io.to('some room').emit('some event');
```

## Different emits

Below are all the different types of emits you can use to get the 'messages' to the clients you want. As you can see there are quite a lot. But they are not overly complicated.

```js
io.on('connect', onConnect);

function onConnect(socket){

  // sending to the client
  socket.emit('hello', 'can you hear me?', 1, 2, 'abc');

  // sending to all clients except sender
  socket.broadcast.emit('broadcast', 'hello friends!');

  // sending to all clients in 'game' room except sender
  socket.to('game').emit('nice game', "let's play a game");

  // sending to all clients in 'game1' and/or in 'game2' room, except sender
  socket.to('game1').to('game2').emit('nice game', "let's play a game (too)");

  // sending to all clients in 'game' room, including sender
  io.in('game').emit('big-announcement', 'the game will start soon');

  // sending to all clients in namespace 'myNamespace', including sender
  io.of('myNamespace').emit('bigger-announcement', 'the tournament will start soon');

  // sending to a specific room in a specific namespace, including sender
  io.of('myNamespace').to('room').emit('event', 'message');

  // sending to individual socketid (private message)
  io.to(`${socketId}`).emit('hey', 'I just met you');

  // WARNING: `socket.to(socket.id).emit()` will NOT work, as it will send to everyone in the room
  // named `socket.id` but the sender. Please use the classic `socket.emit()` instead.

  // sending with acknowledgement
  socket.emit('question', 'do you think so?', function (answer) {});

  // sending without compression
  socket.compress(false).emit('uncompressed', "that's rough");

  // sending a message that might be dropped if the client is not ready to receive messages
  socket.volatile.emit('maybe', 'do you really need it?');

  // specifying whether the data to send has binary data
  socket.binary(false).emit('what', 'I have no binaries!');

  // sending to all clients on this node (when using multiple nodes)
  io.local.emit('hi', 'my lovely babies');

  // sending to all connected clients
  io.emit('an event sent to all connected clients');

};

```

## Coupling with an API

Now we are done with the easy part of socket.io I will explain something a bit more difficult. Coupling your socket.io with a `stream` and getting live data from the twitter API. During a small project I was working I used this method to get the latest tweets and send them to different rooms via socket.io.

First thing first. Connecting with the twitter API. I will not go deeply into the how to get the twitter API connected because that could be a whole new article on its own. [Here](https://developer.twitter.com/en/docs/basics/getting-started) you can find all the things you need to know about connecting to the twitter API. What I also used was a npm package called [twit](https://www.npmjs.com/package/twit)

In the end my server looked like this:

```js
const express = require('express');
const app = express();
const http = require('http').Server(app);
const io = require('socket.io')(http);
const Twit = require('twit')
const Sentiment = require('sentiment');
const sentiment = new Sentiment();
require('dotenv').config()

var T = new Twit({
    consumer_key: process.env.consumer_key,
    consumer_secret: process.env.consumer_secret,
    access_token: process.env.access_token,
    access_token_secret: process.env.access_token_secret
})

app.set("views", "view");
app.set("view engine", "ejs");

app.use(express.static('public'))

app.get('/', index)


function index(req, res) {
    res.render("pages/index");
};

let proTweets = []
let conTweets = []

let stream = T.stream('statuses/filter', { track: '#brexit', language: 'en', tweet_mode: "extended" })

stream.on('tweet', function (stream) {
    streamHandler(stream)
})

```

You can see that through the twit package I was able to create a stream with the twitter API by using `let stream = T.stream('statuses/filter', { track: '#brexit', language: 'en', tweet_mode: "extended" })`. Then using socket like syntax you can call `stream.on`. This means every time a new tweet gets sent, that includes the thing you `track`, something will happen. In this case `streamHandler(stream)` gets called.

In the `streamHandler` function i call `io.to('proBrexit').emit('autoFeed', tweet);`. This means the tweet gets sent to the `proBrexit` room. The only thing you have to do then is to create a listener in the client js that does something when `autoFeed` gets emitted. Like so:

```js

socket.on("autoFeed", function (tweet) {
    document.querySelector(".feed").innerHTML +=
        `<div class="tweet">
            <h3>${tweet.author}</h3>
            <img class="avatar" src="${tweet.avatar}"></img>
            <p>${tweet.body}</p>
        </div>`
})
```
Now every time there is a new tweet it gets added to the feed element. 

## What we have learned

I hope that by reading this article you have some understanding of what socket.io is and what it can do. How to set up a simple chat application for browsers. How different namespaces and rooms can give an extra layer to a chat application and how to implement them. I also hope that you understand that you can do more things with socket.io than only a chat application. And that my example of the twitter/socket.io makes you think of all the awesome things that lay in wait when you start to use socket.io.

Some parts may look complicated but if you start small and go step by step I think you can achieve more than you think. Now start coding!



## Sources
[SOcket.io](https://socket.io/docs/)  
[Twitter API](https://developer.twitter.com/en/docs/basics/getting-started)  
[NPM Twit](https://www.npmjs.com/package/twit)  
